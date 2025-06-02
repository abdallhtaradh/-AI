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
