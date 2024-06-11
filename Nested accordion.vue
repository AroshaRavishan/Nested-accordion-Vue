<script setup>
import { onMounted } from 'vue';
import Preline from 'preline';
import { initFlowbite } from 'flowbite';
import { ref } from 'vue';

const showFullText = ref(false);
const activeTab = ref("Payments");

const { tabArray } = defineProps(['tabArray']);

onMounted(() => {
    initFlowbite();
});

onMounted(() => {
    Preline.init();
});

const selectedFaqIndex = ref(0);
const faqExpanded = ref(false);
const numberToShow = ref(3);
const showViewMore = ref(true);
const details = ref([]); // Initialize as an empty array

const lastOpenedFaqIndex = ref(-1);

const toggleFaqs = () => {
    faqExpanded.value = !faqExpanded.value;
    if (!faqExpanded.value) {
        // If FAQs are collapsed, open the last opened FAQ or the first one if none is opened
        selectedFaqIndex.value = lastOpenedFaqIndex.value !== -1 ? lastOpenedFaqIndex.value : 0;
        // selectedFaqIndex.value = 0;
    } else {
        // If FAQs are expanded, reset selectedFaqIndex
        selectedFaqIndex.value = lastOpenedFaqIndex.value !== -1 ? lastOpenedFaqIndex.value : 0;
    }
    loadMoreFaqs();
};

const toggleAccordion = (index) => {
    if (selectedFaqIndex.value === index) {
        // If the clicked FAQ is already open, close it
        selectedFaqIndex.value = -1;
        lastOpenedFaqIndex.value = -1;
    } else {
        // If the clicked FAQ is closed, open it and update lastOpenedFaqIndex
        lastOpenedFaqIndex.value = index;
        selectedFaqIndex.value = index;
    }
};

const loadMoreFaqs = () => {
    if (faqExpanded.value) {
        numberToShow.value += 6;
        if (numberToShow.value >= details.value.length) {
            // Do not hide the "View More" button when all FAQs are visible
            // showViewMore.value = false;
        }
    } else {
        numberToShow.value = 3;
        // Do not hide the "View More" button when collapsing FAQs
        // showViewMore.value = true;
    }
};
const setTabContent = (tab, content) => {
    activeTab.value = tab;
    details.value = content;
};

// First Tab Load
onMounted(() => {
    setTabContent(tabArray[0].tab, tabArray[0].content);
});

</script>

<template>
    <div class="bg-white mt-20 md:mt-36">
        <div class="container">
            <div class="mx-auto">
                <div class="text-center">
                    <div class="text-2xl sm:text-5xl text-black-700 font-bold my-5">Frequently asked questions</div>
                </div>
                <div class="hidden md:block mt-12">
                    <div class="mb-4 sm:flex justify-center">
                        <ul class="grid sm:flex flex-wrap -mb-px text-sm font-medium text-center gap-7" id="myTab">
                            <!--Content 1-->
                            <li v-for="(faqTab, index) in tabArray" :key="index" class="mr-2" role="presentation">
                                <button @click="setTabContent(faqTab.tab, faqTab.content)"
                                        :class="{ 'active-tab': activeTab === faqTab.tab }"
                                        class="inline-block p-4 border-b-2 border-transparent rounded-t-lg focus:border-primary text-xl !text-black-700 font-medium focus:text-primary hover:!border-primary hover:!text-primary"
                                        type="button">{{faqTab.tab}}
                                </button>
                            </li>
                        </ul>
                    </div>
                    <div id="myTabContent">
                        <div class="py-8 lg:pt-10 lg:pb-0">
                            <div v-for="(detail, index) in details.slice(0, numberToShow)" :key="index" class="border-b my-3">
                                <h2 :id="'accordion-collapse-heading-' + index">
                                    <button type="button" class="flex items-center justify-between w-full p-5 text-base sm:text-xl sm:text-xl font-semibold text-left text-black-700" :data-accordion-target="'#accordion-collapse-body-' + index" :aria-expanded="selectedFaqIndex === index" :aria-controls="'accordion-collapse-body-' + index" @click="toggleAccordion(index)" :class="{ 'text-primary': selectedFaqIndex === index }">
                                        <span>{{ detail.question }}</span>
                                        <svg :class="{ 'rotate-180': selectedFaqIndex === index }" class="w-6 h-6 shrink-0" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg">
                                            <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd"></path>
                                        </svg>
                                    </button>
                                </h2>
                                <div :id="'accordion-collapse-body-' + index" :class="{ hidden: selectedFaqIndex !== index }" :aria-labelledby="'accordion-collapse-heading-' + index">
                                    <div class="p-5">
                                        <p class="text-black-700 font-normal text-base sm:text-xl mb-2">{{ detail.faq_description}}</p>
                                    </div>
                                </div>
                            </div>
                            <button v-if="showViewMore && details.length > 3" class="mt-12 flex justify-center bg-primary rounded-[50px] h-12 w-12 items-center mx-auto text-white text-lg lg:text-2xl text-bold" @click="toggleFaqs">
                                <i :class="['fa-solid fa-angle-down', { 'fa-rotate-180': faqExpanded }]"></i>
                            </button>
                        </div>
                    </div>
                </div>
                <!-- Mobile Nested Accordion -->
                <div class="w-full lg:w-2/3 mx-auto block md:hidden">
                    <div class="hs-accordion-group mt-8">
                        <div v-for="(faqTab, index) in tabArray" :key="index" class="hs-accordion" :id="'hs-basic-nested-heading-' + index">
                            <button @click="setTabContent(faqTab.tab, faqTab.content)"
                                    :class="{ 'active-tab': activeTab === faqTab.tab }"
                                    class="text-lg border-b hs-accordion-active:border-primary text-ash-600 font-semibold hs-accordion-toggle hs-accordion-active:text-primary py-3 inline-flex items-center justify-center w-full text-left transition"
                                    :aria-controls="'hs-basic-nested-collapse-' + index">
                                {{ faqTab.tab }}
                            </button>
                            <div :id="'hs-basic-nested-collapse-' + index" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300"
                                 :aria-labelledby="'hs-basic-nested-heading-' + index">
                                <div class="hs-accordion-group">
                                    <div v-for="(detail, detailIndex) in faqTab.content" :key="detailIndex" class="hs-accordion border-b my-3">
                                        <button class="text-base sm:text-xl font-semibold hs-accordion-toggle text-black-700 hs-accordion-active:text-primary py-3 inline-flex items-center w-full text-left transition"
                                                :aria-controls="'hs-basic-nested-sub-collapse-' + index + '-' + detailIndex">
                                            {{ detail.question }}
                                        </button>
                                        <div :id="'hs-basic-nested-sub-collapse-' + index + '-' + detailIndex" class="hs-accordion-content hidden w-full overflow-hidden transition-[height] duration-300"
                                             :aria-labelledby="'hs-basic-nested-sub-heading-' + index + '-' + detailIndex">
                                            <div class="text-base sm:text-xl text-black-700 pb-3">
                                                {{ detail.faq_description }}
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


<style scoped>
.flex.items-center.justify-between.w-full.p-5.text-base.sm\:text-xl.font-semibold.text-left.text-black-700.bg-gray-100.dark\:bg-gray-800.text-gray-900.dark\:text-white {
    background: transparent;
}

.text-gray-900 {
    --tw-text-opacity: 1;
    color: #8D1CBA !important;
}

.active-tab {
    color: #8D1CBA !important;
    border-bottom-color: #8D1CBA !important;
}
</style>
