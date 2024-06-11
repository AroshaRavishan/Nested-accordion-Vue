<script setup>

import WebLayout from '@/Layouts/WebLayout.vue';
import TabFaq from '@/Components/Web/TabFaq.vue';

const tabArray = [
    { tab: 'Refund', content: [
            { question: 'What is the validity period for requesting a refund?', faq_description: 'Refunds must be requested within a 14-day validity period from the date of purchase. For more detailed information and specific scenarios, please read our complete refund policy.' },
            { question: 'Under what conditions can I be eligible for a refund?', faq_description: 'Eligibility requires no access to course materials, unless there are significant quality or technical issues, which must be sufficiently evidenced. For more detailed information and specific scenarios, please read our complete refund policy.' },
            { question: 'How do I request a refund and what is the processing time?', faq_description: 'Submit requests to info@globaledulink.co.uk or by post within 14 days of purchase. A response will be provided within 3 working days. Refund processing can take up to 30 days. For more detailed information and specific scenarios, please read our complete refund policy.' },
            { question: 'Are there any fees deducted from the refund amount?', faq_description: 'A possible 10% retention fee may apply. For non-UK bank accounts, a 10% processing fee or bank charges, whichever is higher, will be deducted. For more detailed information and specific scenarios, please read our complete refund policy.' },
            { question: 'What are the refund policies for classroom and live online courses?', faq_description: 'Classroom Courses: Full refunds for cancellations made 14 days or more before the course start date; no refund if less than 14 days.\n' +
                    'Live Online Courses: Full refunds for cancellations made within 14 days of booking; no refund if less than 14 days before the course start. For more detailed information and specific scenarios, please read our complete refund policy.' },
        ]},
    { tab: 'Certificate', content: [
            { question: 'What does the Global Edulink e-certificate include?', faq_description: 'It states the course name, accreditation, and award date. A hard copy is also recommended for record safety.' },
            { question: 'Can I get a printed certificate?', faq_description: 'Yes, after course completion, you can purchase a professional hard copy certificate with course details and official hologram.' },
            { question: 'Why is the official certificate important?', faq_description: 'It\'s a professional qualification that enhances job marketability and serves as a record of your skills and commitment.' },
        ]},
    { tab: 'Exam Retake', content: [
            { question: 'What is the policy for retaking an exam if I fail on the first attempt?', faq_description: 'If you fail your exam on the first attempt, you can retake it by paying a Retake Fee. This option is available for a second attempt only.' },
            { question: 'What is the Take2 Exam Option and how does it work?', faq_description: 'Take2 is an add-on for selected exams, available only after an initial exam failure. It\'s non-transferable, non-refundable, and valid for 6 months. It must be bought before the initial exam and can\'t be used if the appointment is missed or not rescheduled.' },
        ]},
    { tab: 'Payment', content: [
            { question: 'What payment methods does Global Edulink accept?', faq_description: 'Payments can be made via Credit Card or Bank Transfer. Contact us for more details.' },

        ]},
    { tab: 'Other', content: [
            { question: 'How can I contact for support?', faq_description: 'You can reach us via phone, WhatsApp, or email. \n' +
                    'Full contact details are provided on our contact page.' },
            { question: 'Where is the head office located?', faq_description: 'Our head office is in London. ' },
            { question: 'What type of queries can I address through the contact form?', faq_description: 'Enquiries about courses, corporate training, customer support, and general feedback can be submitted.' },
            { question: 'Can I communicate in languages other than English?', faq_description: 'Yes, our website offers options for multiple languages, including French, German, Spanish, Arabic, and Hindi.' },
            { question: 'Is there an option to enquire about courses directly through their website?', faq_description: 'Yes, you can submit your queries related to specific courses.' },
            // Add more FAQs for other categories as needed
        ]},
];

</script>

<template>
    <WebLayout>

        <TabFaq :tabArray="tabArray" />

    </WebLayout>
</template>

