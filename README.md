<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>منصة الذكاء الاصطناعي المتكاملة</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Cairo', sans-serif;
        }
        .hero-bg {
            background-image: linear-gradient(to bottom right, #0f172a, #1e293b, #334155);
        }
        .card-hover:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f1f1;
        }
        ::-webkit-scrollbar-thumb {
            background: #3b82f6;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #2563eb;
        }
        .chat-bubble-user {
            background-color: #3b82f6;
            color: white;
            border-radius: 1rem 1rem 0.25rem 1rem;
            align-self: flex-end;
            margin-left: auto;
        }
        .chat-bubble-ai {
            background-color: #e5e7eb;
            color: #1f2937;
            border-radius: 1rem 1rem 1rem 0.25rem;
            align-self: flex-start;
            margin-right: auto;
        }
        .hero-chat-bubble-ai {
            background-color: rgba(229, 231, 235, 0.1);
            color: #e5e7eb;
            border-radius: 1rem 1rem 1rem 0.25rem;
            align-self: flex-start;
            margin-right: auto;
            border: 1px solid rgba(100, 116, 139, 0.5);
        }
        .hero-chat-bubble-user {
            background-color: rgba(59, 130, 246, 0.2);
            color: #eff6ff;
            border-radius: 1rem 1rem 0.25rem 1rem;
            align-self: flex-end;
            margin-left: auto;
            border: 1px solid rgba(59, 130, 246, 0.7);
        }
        .loading-dots span {
            animation: blink 1.4s infinite both;
            display: inline-block;
            width: 6px;
            height: 6px;
            background-color: #9ca3af;
            border-radius: 50%;
            margin: 0 1px;
        }
        .loading-dots.light span {
             background-color: #e5e7eb;
        }
        .loading-dots.blue span {
             background-color: #bfdbfe;
        }
        .loading-dots span:nth-child(2) {
            animation-delay: 0.2s;
        }
        .loading-dots span:nth-child(3) {
            animation-delay: 0.4s;
        }
        @keyframes blink {
            0% { opacity: 0.2; }
            20% { opacity: 1; }
            100% { opacity: 0.2; }
        }
        .game-canvas {
            background-color: #f0f0f0;
            display: block;
            margin: 0 auto;
            border: 2px solid #333;
        }
        .like-btn {
            transition: all 0.3s ease;
        }
        .like-btn:hover {
            transform: scale(1.1);
        }
        .like-btn.liked {
            fill: #ef4444;
            color: #ef4444;
        }
        #generatedImagesContainer img {
            max-height: 300px;
            object-fit: contain;
            background-color: #f5f5f5;
            border: 1px solid #e5e7eb;
        }
    </style>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Cairo', 'sans-serif'],
                    },
                }
            }
        }
    </script>
</head>
<body class="bg-slate-100 text-slate-800">

    <header class="bg-slate-800 text-white shadow-lg sticky top-0 z-50">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <a href="#" class="text-2xl font-bold">
                <span class="text-blue-400">إبداع</span><span class="text-slate-300">AI</span>
            </a>
            <nav class="hidden md:flex space-x-4 space-x-reverse">
                <a href="#home" class="hover:text-blue-300 px-3 py-2 rounded-md">الرئيسية</a>
                <a href="#services" class="hover:text-blue-300 px-3 py-2 rounded-md">خدماتنا</a>
                <a href="#how-it-works" class="hover:text-blue-300 px-3 py-2 rounded-md">كيف نعمل</a>
                <a href="#contact" class="hover:text-blue-300 px-3 py-2 rounded-md">تواصل معنا</a>
            </nav>
            <button id="mobileMenuButton" class="md:hidden text-slate-300 hover:text-white focus:outline-none">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
                </svg>
            </button>
        </div>
        <div id="mobileMenu" class="md:hidden hidden bg-slate-700">
            <a href="#home" class="block px-6 py-3 text-white hover:bg-slate-600">الرئيسية</a>
            <a href="#services" class="block px-6 py-3 text-white hover:bg-slate-600">خدماتنا</a>
            <a href="#how-it-works" class="block px-6 py-3 text-white hover:bg-slate-600">كيف نعمل</a>
            <a href="#contact" class="block px-6 py-3 text-white hover:bg-slate-600">تواصل معنا</a>
        </div>
    </header>

    <section id="home" class="hero-bg text-white py-20 md:py-24">
        <div class="container mx-auto px-6 text-center">
            <h1 class="text-4xl md:text-6xl font-bold mb-6 leading-tight">
                حوّل أفكارك إلى <span class="text-blue-400">واقع ملموس</span>
            </h1>
            <p class="text-lg md:text-xl text-slate-300 mb-10 max-w-3xl mx-auto">
                تفاعل مع منصتنا لوصف مشروعك، وسنقوم بتحليله وإنشاء تصور أولي له أو تعديله حسب طلبك. شاهد أفكارك تنبض بالحياة!
            </p>
            
            <div id="heroCreationChat" class="max-w-2xl mx-auto bg-slate-700/50 backdrop-blur-sm p-6 rounded-xl shadow-2xl">
                <div id="heroChatMessages" class="h-48 overflow-y-auto mb-4 space-y-3 p-3 rounded-lg bg-slate-800/60 text-right">
                    </div>
                <div class="flex space-x-3 space-x-reverse">
                    <input type="text" id="heroChatInput" class="flex-1 p-3 rounded-lg bg-slate-600/70 text-white placeholder-slate-400 focus:ring-2 focus:ring-blue-500 focus:outline-none border border-slate-500" placeholder="صف مشروعك أو اطلب تعديلاً...">
                    <button id="heroSendDescriptionButton" class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-3 px-6 rounded-lg transition duration-300 flex items-center justify-center w-28">
                        <span id="heroSendButtonText">أرسل</span>
                        <div id="heroSendButtonLoading" class="hidden loading-dots light"><span></span><span></span><span></span></div>
                    </button>
                </div>
            </div>
        </div>
    </section>

    <section id="how-it-works" class="py-16 bg-slate-50">
        <div class="container mx-auto px-6">
            <h2 class="text-3xl font-bold text-center mb-12 text-slate-700">كيف نعمل؟ خطوات بسيطة لنتائج مذهلة</h2>
            <div class="grid md:grid-cols-3 gap-8 text-center">
                <div class="bg-white p-8 rounded-xl shadow-lg card-hover transition-all duration-300">
                    <div class="flex justify-center mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-16 h-16 text-blue-500"><path stroke-linecap="round" stroke-linejoin="round" d="M7.5 8.25h9m-9 3H12m-6.75 3h9m-9 3h9M3.75 6.75h16.5v10.5A2.25 2.25 0 0 1 17.25 19.5H6.75A2.25 2.25 0 0 1 4.5 17.25V6.75Z" /></svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-2 text-slate-700">1. صف فكرتك أو اطلب تعديل</h3>
                    <p class="text-slate-600">استخدم واجهة المحادثة في الأعلى لوصف مشروعك الأولي أو لطلب تعديلات على النتائج السابقة.</p>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-lg card-hover transition-all duration-300">
                    <div class="flex justify-center mb-4">
                         <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-16 h-16 text-blue-500"><path stroke-linecap="round" stroke-linejoin="round" d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L1.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09l2.846.813-2.846.813a4.5 4.5 0 0 0-3.09 3.09Z" /></svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-2 text-slate-700">2. نحلل ونُنفذ بذكاء</h3>
                    <p class="text-slate-600">يقوم نظامنا بتحليل طلبك، سواء كان إنشاءً جديدًا أو تعديلاً، وينفذ المطلوب بذكاء، مع إمكانية إضافة وظائف تفاعلية.</p>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-lg card-hover transition-all duration-300">
                    <div class="flex justify-center mb-4">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-16 h-16 text-blue-500"><path stroke-linecap="round" stroke-linejoin="round" d="M3.75 3v11.25A2.25 2.25 0 0 0 6 16.5h12A2.25 2.25 0 0 0 20.25 14.25V3m-16.5 0h16.5m-16.5 0H3.75m16.5 0H20.25M5.625 3v11.25m12.75-11.25v11.25m0 0H5.625m12.75 0h3.75M3 20.25h18M12 3v10.5" /></svg>
                    </div>
                    <h3 class="text-xl font-semibold mb-2 text-slate-700">3. نعرض ونُمكنك من المعاينة</h3>
                    <p class="text-slate-600">شاهد خطة عملك أو موقعك المحدث، وعاينه بشكل تفاعلي مباشرة في مساحة العمل.</p>
                </div>
            </div>
        </div>
    </section>

    <section id="services" class="py-16 bg-white">
        <div class="container mx-auto px-6">
            <h2 class="text-3xl font-bold text-center mb-12 text-slate-700">خدماتنا المبتكرة</h2>
            <div class="grid md:grid-cols-3 gap-8">
                <div class="bg-slate-50 p-8 rounded-xl shadow-lg card-hover transition-all duration-300 flex flex-col">
                    <img src="https://placehold.co/600x400/3b82f6/ffffff?text=إنشاء+مواقع+ويب&font=cairo" alt="[صورة لإنشاء مواقع ويب]" class="rounded-lg mb-6 h-48 w-full object-cover" onerror="this.onerror=null;this.src='https://placehold.co/600x400/cccccc/ffffff?text=Image+Not+Found&font=cairo';">
                    <h3 class="text-2xl font-semibold mb-3 text-slate-700">إنشاء مواقع ويب متكاملة</h3>
                    <p class="text-slate-600 mb-4 flex-grow">حوّل فكرتك إلى موقع ويب احترافي. نُنشئ لك هيكلًا أوليًا يمكنك معاينته وتطويره.</p>
                    <button class="mt-auto bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300 self-start">
                        اكتشف المزيد
                    </button>
                </div>
                <div class="bg-slate-50 p-8 rounded-xl shadow-lg card-hover transition-all duration-300 flex flex-col">
                    <img src="https://placehold.co/600x400/10b981/ffffff?text=تصميم+ألعاب&font=cairo" alt="[صورة لتصميم ألعاب]" class="rounded-lg mb-6 h-48 w-full object-cover" onerror="this.onerror=null;this.src='https://placehold.co/600x400/cccccc/ffffff?text=Image+Not+Found&font=cairo';">
                    <h3 class="text-2xl font-semibold mb-3 text-slate-700">تصميم ألعاب مبتكرة</h3>
                    <p class="text-slate-600 mb-4 flex-grow">نساعدك في وضع تصور وتخطيط لعبتك. أطلق العنان لخيالك ودعنا نهتم بالتفاصيل التقنية.</p>
                     <button class="mt-auto bg-emerald-500 hover:bg-emerald-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300 self-start">
                        اكتشف المزيد
                    </button>
                </div>
                <div class="bg-slate-50 p-8 rounded-xl shadow-lg card-hover transition-all duration-300 flex flex-col">
                    <img src="https://placehold.co/600x400/f59e0b/ffffff?text=توليد+الصور+بالذكاء+الاصطناعي&font=cairo" alt="[صورة لتوليد الصور بالذكاء الاصطناعي]" class="rounded-lg mb-6 h-48 w-full object-cover" onerror="this.onerror=null;this.src='https://placehold.co/600x400/cccccc/ffffff?text=Image+Not+Found&font=cairo';">
                    <h3 class="text-2xl font-semibold mb-3 text-slate-700">توليد الصور بالذكاء الاصطناعي</h3>
                    <p class="text-slate-600 mb-4 flex-grow">أنشئ صورًا فريدة باستخدام الذكاء الاصطناعي بناءً على وصفك النصي. مثالي للتصاميم الفنية، الشعارات، والرسومات المخصصة.</p>
                    <button class="mt-auto bg-amber-500 hover:bg-amber-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300 self-start">
                        اكتشف المزيد
                    </button>
                </div>
            </div>
        </div>
    </section>

    <section id="workspace" class="py-16 bg-slate-200">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-3xl font-bold text-slate-700 mb-6">مساحة العمل والمعاينة</h2>
            <div class="mb-6 flex justify-center space-x-4 space-x-reverse">
                <button id="showWebsiteBtn" class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300">
                    معاينة الموقع
                </button>
                <button id="showGameBtn" class="bg-emerald-500 hover:bg-emerald-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300">
                    معاينة اللعبة
                </button>
                <button id="showImageBtn" class="bg-amber-500 hover:bg-amber-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300">
                    توليد الصور
                </button>
            </div>
            <p class="text-slate-600 mb-8 max-w-xl mx-auto">
                هنا ستظهر نتائج مشروعك بعد وصفه في المحادثة أعلاه.
            </p>
            <div id="previewArea" class="bg-white p-6 md:p-8 rounded-xl shadow-2xl min-h-[300px] flex flex-col items-center justify-start w-full">
                <div id="initialPreviewMessage" class="text-center w-full py-10">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-24 h-24 text-slate-400 mx-auto mb-4">
                        <path stroke-linecap="round" stroke-linejoin="round" d="m2.25 15.75 5.159-5.159a2.25 2.25 0 0 1 3.182 0l5.159 5.159m-1.5-1.5 1.409-1.409a2.25 2.25 0 0 1 3.182 0l2.909 2.909m-18 3.75h16.5a1.5 1.5 0 0 0 1.5-1.5V6a1.5 1.5 0 0 0-1.5-1.5H3.75A1.5 1.5 0 0 0 2.25 6v12a1.5 1.5 0 0 0 1.5 1.5Zm10.5-11.25h.008v.008h-.008V8.25Zm.158 0a.225.225 0 1 1-.45 0 .225.225 0 0 1 .45 0Z" />
                    </svg>
                    <p class="text-xl text-slate-500">معاينة مشروعك ستظهر هنا...</p>
                </div>
                <div id="loadingIndicator" class="hidden mt-4 text-center w-full py-10">
                    <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-blue-500 mx-auto"></div>
                    <p class="text-blue-500 mt-2">جاري معالجة طلبك...</p>
                </div>
                <div id="resultDisplayArea" class="w-full mt-4 hidden">
                    <iframe id="workspacePreviewFrame" class="w-full h-[50vh] md:h-[60vh] border border-slate-300 rounded-md" srcdoc="<p style='text-align:center; padding: 20px; font-family: Cairo, sans-serif;'>سيتم تحميل المعاينة هنا...</p>"></iframe>
                </div>
                <div id="imageGenerationArea" class="w-full mt-4 hidden">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4" id="generatedImagesContainer">
                        <!-- ستظهر الصور المولدة هنا -->
                    </div>
                    <div class="mt-4">
                        <button id="generateMoreImagesBtn" class="bg-amber-500 hover:bg-amber-600 text-white font-semibold py-2 px-6 rounded-lg transition duration-300 hidden">
                            توليد المزيد من الصور
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </section>
    
    <div id="aiAssistantButton" class="fixed bottom-6 left-6 bg-blue-600 text-white p-4 rounded-full shadow-xl cursor-pointer hover:bg-blue-700 transition-colors z-40">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-8 h-8">
            <path stroke-linecap="round" stroke-linejoin="round" d="M8.625 12a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm0 0H8.25m4.125 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm0 0H12m4.125 0a.375.375 0 1 1-.75 0 .375.375 0 0 1 .75 0Zm0 0h-.375M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z" />
        </svg>
    </div>

    <div id="aiAssistantChatbox" class="hidden fixed bottom-24 left-6 w-80 md:w-96 bg-white rounded-xl shadow-2xl overflow-hidden z-50 flex flex-col">
        <div class="bg-blue-600 text-white p-4 flex justify-between items-center">
            <h3 class="font-semibold">مساعدك الذكي</h3>
            <button id="closeChatbox" class="text-white hover:text-blue-200">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
                </svg>
            </button>
        </div>
        <div id="chatMessages" class="p-4 h-64 overflow-y-auto space-y-3 flex-grow flex flex-col text-right">
            </div>
        <div id="chatLoadingIndicator" class="hidden p-3 chat-bubble-ai max-w-[85%] self-start">
            <div class="loading-dots"><span></span><span></span><span></span></div>
        </div>
        <div class="p-4 border-t border-slate-200 bg-slate-50">
            <div class="flex space-x-2 space-x-reverse">
                <input type="text" id="chatInput" class="flex-1 p-2 border border-slate-300 rounded-lg focus:ring-1 focus:ring-blue-500 focus:outline-none" placeholder="اكتب رسالتك...">
                <button id="sendChatMessage" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg flex items-center justify-center">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-5 h-5">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M6 12L3.269 3.126A59.768 59.768 0 0 1 21.485 12 59.77 59.77 0 0 1 3.27 20.876L5.999 12zm0 0h7.5" />
                    </svg>
                </button>
            </div>
        </div>
    </div>

    <section id="contact" class="py-16 bg-slate-800 text-white">
        <div class="container mx-auto px-6 text-center">
            <h2 class="text-3xl font-bold mb-6">هل لديك أسئلة؟ تواصل معنا!</h2>
            <p class="text-slate-300 mb-8 max-w-xl mx-auto">
                فريقنا مستعد للإجابة على جميع استفساراتك ومساعدتك في بدء مشروعك القادم.
            </p>
            <a href="mailto:info@ebda3.ai" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-3 px-8 rounded-lg text-lg shadow-md transition duration-300 transform hover:scale-105">
                تواصل عبر البريد الإلكتروني
            </a>
        </div>
    </section>

    <footer class="bg-slate-900 text-slate-400 py-10 text-center">
        <div class="container mx-auto px-6">
            <p>&copy; <span id="currentYear"></span> منصة إبداعAI. جميع الحقوق محفوظة.</p>
            <p class="text-sm mt-2">
                <a href="#" class="hover:text-blue-400">سياسة الخصوصية</a> | 
                <a href="#" class="hover:text-blue-400">شروط الخدمة</a>
            </p>
        </div>
    </footer>

    <div id="customAlertModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-[100] hidden">
        <div class="bg-white p-6 rounded-lg shadow-xl max-w-sm w-full text-center">
            <h3 id="customAlertTitle" class="text-xl font-semibold mb-4 text-slate-700">تنبيه</h3>
            <p id="customAlertMessage" class="text-slate-600 mb-6"></p>
            <button id="customAlertCloseButton" class="bg-blue-500 hover:bg-blue-600 text-white font-semibold py-2 px-6 rounded-lg">
                موافق
            </button>
        </div>
    </div>

    <script>
        // --- Global Variables & API Configuration ---
        const GEMINI_API_KEY = ""; // IMPORTANT: Leave empty, Canvas will provide it.
        const GEMINI_API_URL_FLASH = `https://generativelanguage.googleapis.com/v1beta/models/gemini-2.0-flash:generateContent?key=${GEMINI_API_KEY}`;
        const IMAGE_GENERATION_API_KEY = ""; // أضف مفتاح API لتوليد الصور هنا
        
        // --- UI Elements ---
        const mobileMenuButton = document.getElementById('mobileMenuButton');
        const mobileMenu = document.getElementById('mobileMenu');
        
        // Hero Creation Chat UI
        const heroChatMessages = document.getElementById('heroChatMessages');
        const heroChatInput = document.getElementById('heroChatInput');
        const heroSendDescriptionButton = document.getElementById('heroSendDescriptionButton');
        const heroSendButtonText = document.getElementById('heroSendButtonText');
        const heroSendButtonLoading = document.getElementById('heroSendButtonLoading');

        // Workspace & Preview UI
        const initialPreviewMessage = document.getElementById('initialPreviewMessage');
        const loadingIndicator = document.getElementById('loadingIndicator'); 
        const resultDisplayArea = document.getElementById('resultDisplayArea');
        const workspacePreviewFrame = document.getElementById('workspacePreviewFrame');
        const showWebsiteBtn = document.getElementById('showWebsiteBtn');
        const showGameBtn = document.getElementById('showGameBtn');
        const showImageBtn = document.getElementById('showImageBtn');
        const imageGenerationArea = document.getElementById('imageGenerationArea');
        const generatedImagesContainer = document.getElementById('generatedImagesContainer');
        const generateMoreImagesBtn = document.getElementById('generateMoreImagesBtn');

        // General AI Assistant Chat UI (bottom-left)
        const aiAssistantButton = document.getElementById('aiAssistantButton');
        const aiAssistantChatbox = document.getElementById('aiAssistantChatbox');
        const closeChatbox = document.getElementById('closeChatbox');
        const chatMessages = document.getElementById('chatMessages'); 
        const chatInput = document.getElementById('chatInput'); 
        const sendChatMessage = document.getElementById('sendChatMessage'); 
        const chatLoadingIndicator = document.getElementById('chatLoadingIndicator'); 
        
        // Modals
        const customAlertModal = document.getElementById('customAlertModal');
        const customAlertTitle = document.getElementById('customAlertTitle');
        const customAlertMessage = document.getElementById('customAlertMessage');
        const customAlertCloseButton = document.getElementById('customAlertCloseButton');

        // --- State Variables ---
        let currentMode = 'website'; // 'website' or 'game' or 'image'
        let generatedHtmlContent = ""; 
        let generatedGameContent = "";
        let generatedImages = [];
        let heroChatHistory = []; 
        let generalChatHistory = []; 
        let isProjectInitiated = false; 

        // --- Helper Functions ---
        function showCustomAlert(message, title = "تنبيه") {
            customAlertTitle.textContent = title;
            customAlertMessage.textContent = message;
            customAlertModal.classList.remove('hidden');
        }

        function addMessageToHeroChat(message, sender) {
            const messageDiv = document.createElement('div');
            messageDiv.classList.add('p-3', 'max-w-[85%]', 'text-sm', 'whitespace-pre-wrap', 'rounded-lg', 'break-words');
            if (sender === 'user') {
                messageDiv.classList.add('hero-chat-bubble-user');
            } else { 
                messageDiv.classList.add('hero-chat-bubble-ai');
            }
            messageDiv.textContent = message; 
            heroChatMessages.appendChild(messageDiv);
            heroChatMessages.scrollTop = heroChatMessages.scrollHeight;
        }

        function addMessageToGeneralChat(message, sender, isInitial = false) {
            if(!isInitial) {
                const initialGreetingElement = document.getElementById('initialAiGreeting');
                if (initialGreetingElement) {
                    initialGreetingElement.remove();
                }
            }

            const messageDiv = document.createElement('div');
            messageDiv.classList.add('p-3', 'max-w-[85%]', 'text-sm', 'whitespace-pre-wrap', 'rounded-lg', 'break-words');
             if (sender === 'user') {
                messageDiv.classList.add('chat-bubble-user');
            } else { 
                messageDiv.classList.add('chat-bubble-ai');
                if(isInitial) messageDiv.id = 'initialAiGreeting'; 
            }
            messageDiv.textContent = message; 
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight; 
        }

        // --- Gemini API Call Function ---
        async function callGeminiAPI(promptText, currentChatHistory = []) {
            let apiHistory = [];
            currentChatHistory.forEach(item => {
                apiHistory.push({ role: item.role, parts: [{ text: item.parts[0].text }] });
            });

            if (promptText) { 
                 apiHistory.push({ role: "user", parts: [{ text: promptText }] });
            }
            
            const payload = { contents: apiHistory };
            try {
                const response = await fetch(GEMINI_API_URL_FLASH, {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(payload)
                });
                if (!response.ok) {
                    const errorData = await response.json();
                    console.error("Gemini API Error:", errorData);
                    const specificMessage = errorData?.error?.message || `API Error: ${response.status} ${response.statusText}`;
                    throw new Error(specificMessage);
                }
                const result = await response.json();
                if (result.candidates && result.candidates.length > 0 &&
                    result.candidates[0].content && result.candidates[0].content.parts &&
                    result.candidates[0].content.parts.length > 0) {
                    const aiTextResponse = result.candidates[0].content.parts[0].text;
                    return aiTextResponse;
                } else {
                    console.error("Unexpected API response structure:", result);
                    throw new Error("لم يتم العثور على محتوى في رد الـ API.");
                }
            } catch (error) {
                console.error("Error calling Gemini API:", error);
                throw error; 
            }
        }

        // --- Image Generation Function ---
        async function generateAIImages(prompt) {
            try {
                // في الواقع العملي، استبدل هذا بالاتصال بخدمة توليد الصور مثل DALL-E أو Stable Diffusion
                // هذا مثال وهمي للتوضيح فقط
                showCustomAlert("هذه ميزة تجريبية. في التطبيق الحقيقي، سيتم الاتصال بخدمة توليد الصور مثل DALL-E أو Stable Diffusion API.", "تجريبي");
                
                // مثال: إنشاء صور وهمية للعرض التوضيحي
                const mockImages = [
                    "https://placehold.co/600x400/3b82f6/ffffff?text=صورة+مولدة+1&font=cairo",
                    "https://placehold.co/600x400/10b981/ffffff?text=صورة+مولدة+2&font=cairo",
                    "https://placehold.co/600x400/f59e0b/ffffff?text=صورة+مولدة+3&font=cairo",
                    "https://placehold.co/600x400/8b5cf6/ffffff?text=صورة+مولدة+4&font=cairo"
                ];
                
                return mockImages;
            } catch (error) {
                console.error("Error generating images:", error);
                throw error;
            }
        }

        function displayGeneratedImages(images) {
            const container = document.getElementById('generatedImagesContainer');
            container.innerHTML = '';
            
            images.forEach(imgUrl => {
                const imgDiv = document.createElement('div');
                imgDiv.className = 'bg-white p-4 rounded-lg shadow-md';
                imgDiv.innerHTML = `
                    <img src="${imgUrl}" alt="صورة مولدة بالذكاء الاصطناعي" class="w-full h-auto rounded-md mb-2">
                    <div class="flex justify-between items-center">
                        <a href="${imgUrl}" download="ai-generated-image" class="text-blue-500 hover:text-blue-700">
                            تحميل
                        </a>
                        <button class="text-amber-500 hover:text-amber-700 like-btn">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />
                            </svg>
                        </button>
                    </div>
                `;
                container.appendChild(imgDiv);
            });
            
            document.getElementById('generateMoreImagesBtn').classList.remove('hidden');
        }

        // --- Hero Creation Chat Logic ---
        let isProcessingHeroRequest = false; 
        async function handleHeroSendDescription() {
            if (isProcessingHeroRequest) return;
            const userMessage = heroChatInput.value.trim(); 
            if (userMessage === "") {
                showCustomAlert("الرجاء وصف مشروعك أو طلب التعديل في حقل الإدخال.");
                return;
            }

            addMessageToHeroChat(userMessage, 'user');
            heroChatHistory.push({ role: "user", parts: [{ text: userMessage }] });
            heroChatInput.value = '';

            isProcessingHeroRequest = true;
            heroSendButtonText.classList.add('hidden');
            heroSendButtonLoading.classList.remove('hidden');
            
            // Prepare UI for new result
            initialPreviewMessage.classList.add('hidden');
            loadingIndicator.classList.remove('hidden'); 
            resultDisplayArea.classList.add('hidden');
            imageGenerationArea.classList.add('hidden');
            workspacePreviewFrame.classList.add('hidden');
            workspacePreviewFrame.srcdoc = "<p style='text-align:center; padding: 20px; font-family: Cairo, sans-serif;'>سيتم تحميل المعاينة هنا...</p>";

            document.getElementById('workspace').scrollIntoView({ behavior: 'smooth' });

            let promptForThisTurn; 
            let historyForGeminiCall = heroChatHistory.slice(0, -1); 

            if (!isProjectInitiated) {
                if (currentMode === 'website') {
                    promptForThisTurn = `
أنت مساعد ذكاء اصطناعي متقدم في منصة "إبداعAI". مهمتك هي تحليل وصف مشروع المستخدم الأولي.
وصف المشروع من المستخدم: "${userMessage}"

1. إذا كان الوصف يشير بوضوح إلى طلب إنشاء **موقع ويب**:
   * قم بإنشاء **كود HTML أساسي لصفحة واحدة** يمثل هيكلًا أوليًا لهذا الموقع.
   * يجب أن يتضمن الكود:
     * \`<!DOCTYPE html>\`
     * \`<html>\` مع \`lang="ar"\` و \`dir="rtl"\`
     * \`<head>\` مع \`<meta charset="UTF-8">\`, \`<meta name="viewport" content="width=device-width, initial-scale=1.0">\`, \`<title>\` (مستوحى من الوصف), وبعض التنسيقات الأساسية المضمنة (مثال: \`<style>body { font-family: 'Cairo', Arial, sans-serif; direction: rtl; text-align: right; padding: 20px; line-height: 1.6; color: #333; background-color: #f4f4f9; } h1 { color: #0056b3; text-align: center; } p { margin-bottom: 1em; } .container { max-width: 800px; margin: 20px auto; background: #ffffff; padding: 25px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); } img { max-width: 100%; height: auto; border-radius: 4px; margin-bottom: 1em;} footer { text-align: center; margin-top: 30px; font-size: 0.9em; color: #777; }</style>\`) لجعل المعاينة تبدو معقولة واحترافية.
     * \`<body>\` مع \`<div class="container">\` يحتوي على عنوان رئيسي \`<h1>\` وفقرة \`<p>\` واحدة على الأقل تعكس محتوى الموقع المطلوب بناءً على وصف المستخدم. يمكنك إضافة صورة placeholder إذا كان ذلك مناسبًا (مثال: \`<img src="https://placehold.co/600x300/0056b3/ffffff?text=محتوى+الموقع&font=cairo" alt="صورة توضيحية">\`). أضف قسم \`<footer>\` بسيط.
     * **إذا كان وصف المستخدم يتضمن عناصر تفاعلية (مثل أزرار تقوم بوظائف، عدادات، نوافذ منبثقة بسيطة، إلخ)، حاول تضمين JavaScript أساسي ومضمن (\` <script>...\script> \`) لجعل هذه العناصر تعمل بشكل مبدئي.** استخدم معالجات الأحداث (event listeners) بشكل مناسب. **تجنب استخدام \`alert()\`**، وبدلاً من ذلك، إذا كنت بحاجة إلى إظهار رسالة، قم بتحديث محتوى عنصر HTML موجود أو قم بإنشاء عنصر جديد لعرض الرسالة.
   * **يجب أن يكون ردك هو كود HTML فقط، بدون أي نصوص أو تفسيرات إضافية قبله أو بعده.** تأكد أن الكود يبدأ بـ \`<!DOCTYPE html>\`.
2. إذا كان الوصف **لا يشير** إلى إنشاء موقع ويب (مثل طلب لعبة، تطبيق، أو خطة عامة):
   * قم بإنشاء لعبة ويب بسيطة باستخدام HTML و JavaScript فقط.
   * يجب أن يتضمن الكود:
     * \`<!DOCTYPE html>\`
     * \`<html>\` مع \`lang="ar"\` و \`dir="rtl"\`
     * تنسيقات CSS مدمجة لجعل اللعبة جذابة
     * منطق اللعبة باستخدام JavaScript مدمج
   * أنواع الألعاب المحتملة:
     - ألعاب المنصات البسيطة
     - ألعاب الألغاز
     - ألعاب الذاكرة
     - ألعاب القفز
     - ألعاب التصويب البسيطة
   * يجب أن تحتوي اللعبة على:
     - واجهة واضحة
     - نظام نقاط أو مستوى
     - تعليمات بسيطة
   * استخدم العناصر التالية حسب الحاجة:
     - canvas لرسم اللعبة
     - عناصر DOM للتحكم
     - event listeners للتفاعل
   * **يجب أن يكون ردك هو كود HTML فقط يبدأ بـ <!DOCTYPE html> بدون أي نصوص إضافية**
   * إذا كان الوصف غامضًا، قم بإنشاء لعبة ذاكرة بسيطة أو لعبة منصات أساسية

الرجاء تقديم ردك بناءً على هذه التعليمات.`;
                } else if (currentMode === 'game') {
                    promptForThisTurn = `
أنت مساعد ذكاء اصطناعي متخصص في إنشاء ألعاب ويب بسيطة. مهمتك هي تحويل وصف اللعبة من المستخدم إلى كود HTML و JavaScript يعمل.

وصف اللعبة من المستخدم: "${userMessage}"

1. قم بإنشاء لعبة ويب بسيطة باستخدام HTML و JavaScript فقط.
2. يجب أن يتضمن الكود:
   * \`<!DOCTYPE html>\`
   * \`<html>\` مع \`lang="ar"\` و \`dir="rtl"\`
   * تنسيقات CSS مدمجة لجعل اللعبة جذابة
   * منطق اللعبة باستخدام JavaScript مدمج
3. أنواع الألعاب المحتملة:
   - ألعاب المنصات البسيطة
   - ألعاب الألغاز
   - ألعاب الذاكرة
   - ألعاب القفز
   - ألعاب التصويب البسيطة
4. يجب أن تحتوي اللعبة على:
   - واجهة واضحة
   - نظام نقاط أو مستوى
   - تعليمات بسيطة
5. استخدم العناصر التالية حسب الحاجة:
   - canvas لرسم اللعبة
   - عناصر DOM للتحكم
   - event listeners للتفاعل
6. **يجب أن يكون ردك هو كود HTML فقط يبدأ بـ <!DOCTYPE html> بدون أي نصوص إضافية**
7. إذا كان الوصف غامضًا، قم بإنشاء لعبة ذاكرة بسيطة أو لعبة منصات أساسية
`;
                } else if (currentMode === 'image') {
                    promptForThisTurn = `
أنت مساعد توليد صور بالذكاء الاصطناعي. مهمتك هي تحويل وصف المستخدم إلى مواصفات دقيقة لإنشاء الصور.
وصف الصورة من المستخدم: "${userMessage}"

1. قم بتحليل الوصف وتحديد العناصر الرئيسية للصورة
2. أنشئ مواصفات دقيقة للصورة تشمل:
   - الموضوع الرئيسي
   - الألوان المطلوبة
   - النمط الفني (واقعي، كاريكاتير، انطباعي، إلخ)
   - أي تفاصيل إضافية
3. يجب أن يكون الرد باللغة الإنجليزية ليتوافق مع واجهات برمجة التطبيقات لتوليد الصور
4. لا تقدم أي تفسيرات إضافية، فقط أعط المواصفات باللغة الإنجليزية

Example response:
"A beautiful sunset over desert with palm trees, arabic style architecture in background, vibrant colors, digital art style"
`;
                }
            } else {
                if (currentMode === 'website') {
                    promptForThisTurn = `
أنت مساعد تعديل لمشروع تم إنشاؤه مسبقًا في منصة "إبداعAI".
مهمتك هي فهم طلب التعديل من المستخدم وتطبيق التغييرات المطلوبة على الناتج السابق (كود HTML) الموجود في سجل المحادثة.
الناتج السابق (HTML) موجود ضمن رسائل "model" في سجل المحادثة. طلب المستخدم الحالي هو "${userMessage}".
تعليمات هامة:
1. **راجع سجل المحادثة بالكامل** لفهم السياق والمخرجات السابقة.
2. **يجب أن يكون ردك هو كود HTML الكامل والمعدل، متضمنًا أي JavaScript ضروري داخل وسوم \`<script>\`** . لا تقم فقط بوصف التغييرات أو تقديم أجزاء من الكود. تأكد أن الكود يبدأ بـ \`<!DOCTYPE html>\`. **تجنب استخدام \`alert()\`**، واستخدم بدائل لتحديث DOM لعرض الرسائل.
3. إذا كان طلب التعديل غامضًا، قم بإجراء تعديلات بسيطة على النص أو الألوان مع الحفاظ على هيكل الصفحة.
4. لا تقدم أي تفسيرات نصية، فقط أعد كود HTML المعدل.
`;
                } else if (currentMode === 'game') {
                    promptForThisTurn = `
أنت مساعد لتعديل الألعاب في منصة "إبداعAI". 
المطلوب هو تعديل اللعبة الحالية بناءً على طلب المستخدم: "${userMessage}"

النقاط المهمة:
1. راجع سجل المحادثة للعثور على كود اللعبة الحالي
2. قم بالتعديلات المطلوبة مع الحفاظ على عمل اللعبة
3. يمكنك إضافة:
   - مستويات جديدة
   - شخصيات جديدة
   - تحديات إضافية
   - تحسينات بصرية
4. تأكد من بقاء الكود يعمل بشكل صحيح
5. **أعد كود HTML كامل مع JavaScript المدمج فقط، بدون أي تفسيرات**
6. تأكد أن الكود يبدأ بـ <!DOCTYPE html>
`;
                } else if (currentMode === 'image') {
                    promptForThisTurn = `
أنت مساعد لتعديل مواصفات الصور في منصة "إبداعAI".
المطلوب هو تعديل مواصفات الصور بناءً على طلب المستخدم: "${userMessage}"

النقاط المهمة:
1. راجع سجل المحادثة للعثور على مواصفات الصور الحالية
2. قم بالتعديلات المطلوبة مع الحفاظ على الجودة
3. يمكنك إضافة:
   - تفاصيل جديدة
   - تغيير النمط الفني
   - تعديل الألوان
4. **أعد المواصفات الجديدة باللغة الإنجليزية فقط، بدون أي تفسيرات**
`;
                }
            }
            
            try {
                const aiResponse = await callGeminiAPI(promptForThisTurn, historyForGeminiCall);
                
                loadingIndicator.classList.add('hidden');

                if (currentMode === 'image') {
                    // توليد الصور
                    const images = await generateAIImages(aiResponse);
                    generatedImages = images;
                    
                    imageGenerationArea.classList.remove('hidden');
                    displayGeneratedImages(generatedImages);
                    
                } else if (aiResponse.trim().toLowerCase().startsWith("<!doctype html>")) {
                    // إنشاء أو تعديل موقع/لعبة
                    resultDisplayArea.classList.remove('hidden');
                    
                    if (currentMode === 'website') {
                        generatedHtmlContent = aiResponse;
                    } else {
                        generatedGameContent = aiResponse;
                    }
                    
                    workspacePreviewFrame.srcdoc = currentMode === 'website' ? generatedHtmlContent : generatedGameContent;
                    workspacePreviewFrame.classList.remove('hidden');
                } else {
                    const htmlMatch = aiResponse.match(/<!DOCTYPE html>[\s\S]*<\/html>/i);
                    if (htmlMatch) {
                        resultDisplayArea.classList.remove('hidden');
                        
                        if (currentMode === 'website') {
                            generatedHtmlContent = htmlMatch[0];
                        } else {
                            generatedGameContent = htmlMatch[0];
                        }
                        workspacePreviewFrame.srcdoc = htmlMatch[0];
                        workspacePreviewFrame.classList.remove('hidden');
                    } else {
                        workspacePreviewFrame.srcdoc = `
                            <div style="font-family: 'Cairo', sans-serif; direction: rtl; text-align: center; padding: 40px;">
                                <h1 style="color: #dc2626;">عذراً، حدث خطأ</h1>
                                <p>لم نتمكن من إنشاء معاينة HTML لطلبك. الرجاء المحاولة مرة أخرى.</p>
                            </div>
                        `;
                        workspacePreviewFrame.classList.remove('hidden');
                    }
                }

                isProjectInitiated = true;

            } catch (error) {
                loadingIndicator.classList.add('hidden');
                workspacePreviewFrame.srcdoc = `
                    <div style="font-family: 'Cairo', sans-serif; direction: rtl; text-align: center; padding: 40px;">
                        <h1 style="color: #dc2626;">عذراً، حدث خطأ</h1>
                        <p>${error.message}</p>
                        <p>الرجاء المحاولة مرة أخرى.</p>
                    </div>
                `;
                workspacePreviewFrame.classList.remove('hidden');
            } finally {
                heroSendButtonText.classList.remove('hidden');
                heroSendButtonLoading.classList.add('hidden');
                isProcessingHeroRequest = false;
                heroChatInput.focus();
            }
        }

        heroSendDescriptionButton.addEventListener('click', handleHeroSendDescription);
        heroChatInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) { 
                e.preventDefault();
                handleHeroSendDescription();
            }
        });

        // --- Toggle between Website, Game and Image modes ---
        showWebsiteBtn.addEventListener('click', () => {
            currentMode = 'website';
            if (generatedHtmlContent) {
                workspacePreviewFrame.srcdoc = generatedHtmlContent;
                workspacePreviewFrame.classList.remove('hidden');
                resultDisplayArea.classList.remove('hidden');
                imageGenerationArea.classList.add('hidden');
                initialPreviewMessage.classList.add('hidden');
            } else {
                showCustomAlert("لم يتم إنشاء موقع ويب بعد. الرجاء وصف موقعك أولاً.");
            }
        });

        showGameBtn.addEventListener('click', () => {
            currentMode = 'game';
            if (generatedGameContent) {
                workspacePreviewFrame.srcdoc = generatedGameContent;
                workspacePreviewFrame.classList.remove('hidden');
                resultDisplayArea.classList.remove('hidden');
                imageGenerationArea.classList.add('hidden');
                initialPreviewMessage.classList.add('hidden');
            } else {
                showCustomAlert("لم يتم إنشاء لعبة بعد. الرجاء وصف لعبتك أولاً.");
            }
        });

        showImageBtn.addEventListener('click', () => {
            currentMode = 'image';
            if (generatedImages.length > 0) {
                imageGenerationArea.classList.remove('hidden');
                resultDisplayArea.classList.add('hidden');
                workspacePreviewFrame.classList.add('hidden');
                initialPreviewMessage.classList.add('hidden');
                displayGeneratedImages(generatedImages);
            } else {
                showCustomAlert("لم يتم توليد أي صور بعد. الرجاء وصف الصورة التي تريدها في المحادثة.");
            }
        });

        generateMoreImagesBtn.addEventListener('click', async () => {
            const lastPrompt = heroChatHistory[heroChatHistory.length - 2].parts[0].text;
            try {
                const newImages = await generateAIImages(lastPrompt);
                generatedImages = [...generatedImages, ...newImages];
                displayGeneratedImages(generatedImages);
            } catch (error) {
                showCustomAlert("حدث خطأ أثناء توليد صور إضافية. الرجاء المحاولة مرة أخرى.");
            }
        });

        // --- AI Assistant Chatbox Logic ---
        aiAssistantButton.addEventListener('click', () => {
            aiAssistantChatbox.classList.toggle('hidden');
            if (!aiAssistantChatbox.classList.contains('hidden')) {
                 chatInput.focus(); 
                if (chatMessages.children.length === 0 || (chatMessages.children.length === 1 && chatMessages.children[0].id === 'initialAiGreeting')) {
                    addMessageToGeneralChat("مرحباً! أنا مساعدك الذكي. كيف يمكنني مساعدتك اليوم؟", 'ai', true);
                }
            }
        });

        closeChatbox.addEventListener('click', () => {
            aiAssistantChatbox.classList.add('hidden');
        });

        let isGeneralChatProcessing = false;
        async function handleSendChatMessage() {
            if(isGeneralChatProcessing) return;
            const userMessage = chatInput.value.trim();
            if (userMessage === "") return;

            addMessageToGeneralChat(userMessage, 'user');
            generalChatHistory.push({ role: "user", parts: [{ text: userMessage }] });
            chatInput.value = '';
            
            isGeneralChatProcessing = true;
            chatLoadingIndicator.classList.remove('hidden');
            chatMessages.scrollTop = chatMessages.scrollHeight; 

            const generalAssistantSystemPrompt = `أنت مساعد ذكاء اصطناعي عام لمنصة "إبداعAI". مهمتك هي مساعدة المستخدمين والإجابة على استفساراتهم حول المنصة، أو تقديم مساعدة عامة. كن ودودًا ومفيدًا.`;
            let historyForGeneralApiCall = generalChatHistory.slice(0, -1); 
            const promptForGeneralApiTurn = `${generalAssistantSystemPrompt}\n\nاستفسار المستخدم: "${userMessage}"`;

            try {
                const aiResponse = await callGeminiAPI(promptForGeneralApiTurn, historyForGeneralApiCall); 
                addMessageToGeneralChat(aiResponse, 'ai');
                generalChatHistory.push({ role: "model", parts: [{ text: aiResponse }] });
            } catch (error) {
                const errorMsgForChat = `عذراً، حدث خطأ: ${error.message}. حاول مرة أخرى.`;
                addMessageToGeneralChat(errorMsgForChat, 'ai');
                generalChatHistory.push({ role: "model", parts: [{ text: errorMsgForChat }] });
            } finally {
                chatLoadingIndicator.classList.add('hidden');
                isGeneralChatProcessing = false;
                chatInput.focus();
            }
        }

        sendChatMessage.addEventListener('click', handleSendChatMessage);
        chatInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                handleSendChatMessage();
            }
        });

        // Ensure smooth scroll for navigation links
        document.querySelectorAll('header nav a[href^="#"], header div#mobileMenu a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement) {
                    if (mobileMenu.contains(this) && !mobileMenu.classList.contains('hidden')) {
                         mobileMenu.classList.add('hidden');
                    }
                    targetElement.scrollIntoView({
                        behavior: 'smooth'
                    });
                }
            });
        });

        // Initialize current year
        document.getElementById('currentYear').textContent = new Date().getFullYear();

        // Initialize chat history
        const initialHeroPromptText = "مرحباً بك في منصة إبداعAI! صف لي فكرة مشروعك هنا (موقع ويب أو لعبة أو صورة)، وسأساعدك في تحويلها إلى واقع أو تعديلها حسب طلبك.";
        addMessageToHeroChat(initialHeroPromptText, 'ai');
        heroChatHistory.push({ role: "model", parts: [{ text: initialHeroPromptText }]});

        const initialGeneralAssistantMessage = "مرحباً! أنا مساعدك الذكي. كيف يمكنني مساعدتك اليوم؟";
        if (generalChatHistory.length === 0) { 
             generalChatHistory.push({ role: "model", parts: [{ text: initialGeneralAssistantMessage }] });
        }

        // Handle like buttons for generated images (delegated event)
        document.addEventListener('click', function(e) {
            if (e.target.closest('.like-btn')) {
                const likeBtn = e.target.closest('.like-btn');
                likeBtn.classList.toggle('liked');
                
                const svg = likeBtn.querySelector('svg');
                if (likeBtn.classList.contains('liked')) {
                    svg.innerHTML = '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" fill="currentColor"/>';
                } else {
                    svg.innerHTML = '<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z" />';
                }
            }
        });

        // Handle custom alert close
        customAlertCloseButton.addEventListener('click', () => {
            customAlertModal.classList.add('hidden');
        });

        // Handle mobile menu toggle
        mobileMenuButton.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });
    </script>
</body>
</html>
