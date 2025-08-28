<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>بنر ساز حرفه‌ای</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://html2canvas.hertzen.com/dist/html2canvas.min.js"></script>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    @font-face {
      font-family: 'Vazir';
      src: url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.ttf');
    }
    * {
      font-family: 'Vazir', sans-serif;
    }
    
    /* استایل‌های کلی */
    body {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      padding: 0;
      margin: 0;
    }
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 15px;
    }
    .header {
      background: rgba(255, 255, 255, 0.9);
      border-radius: 15px;
      padding: 15px;
      margin-bottom: 20px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    }
    .tabs-container {
      display: flex;
      background: white;
      border-radius: 12px;
      padding: 10px;
      margin-bottom: 20px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      overflow-x: auto;
    }
    .tab {
      padding: 12px 20px;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.3s ease;
      white-space: nowrap;
      display: flex;
      align-items: center;
      gap: 8px;
      margin: 0 5px;
    }
    .tab.active {
      background: #3b82f6;
      color: white;
      box-shadow: 0 4px 6px rgba(59, 130, 246, 0.4);
    }
    .tab:hover:not(.active) {
      background: #f1f5f9;
    }
    .page {
      display: none;
      background: white;
      border-radius: 15px;
      padding: 20px;
      box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
      margin-bottom: 20px;
      min-height: 500px;
    }
    .page.active {
      display: block;
      animation: fadeIn 0.3s ease;
    }
    .ai-fullscreen {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: 1000;
      background: #0d1117;
      display: none;
      flex-direction: column;
    }
    .ai-fullscreen.active {
      display: flex;
    }
    .ai-header {
      background: #161b22;
      padding: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid #30363d;
    }
    .ai-close {
      background: #58a6ff;
      color: white;
      border: none;
      border-radius: 5px;
      padding: 8px 15px;
      cursor: pointer;
      font-size: 14px;
    }
    .ai-content {
      flex: 1;
      display: flex;
      flex-direction: column;
      overflow: hidden;
    }
    .ai-chat-container {
      flex: 1;
      display: flex;
      flex-direction: column;
      overflow: hidden;
    }
    .ai-chat-window {
      flex: 1;
      overflow-y: auto;
      padding: 15px;
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    .ai-message {
      max-width: 85%;
      padding: 12px 16px;
      border-radius: 12px;
      line-height: 1.4;
      white-space: pre-wrap;
      position: relative;
      animation: fadeIn 0.3s ease-in-out;
      word-break: break-word;
      font-size: 15px;
      display: flex;
      align-items: flex-start;
      gap: 8px;
    }
    .ai-user {
      background: #238636;
      color: #fff;
      align-self: flex-end;
      border-bottom-right-radius: 0;
    }
    .ai-bot {
      background: rgba(33, 38, 45, 0.9);
      color: #fff;
      align-self: flex-start;
      border-bottom-left-radius: 0;
    }
    .ai-input-area {
      display: flex;
      padding: 12px;
      border-top: 1px solid #30363d;
      background: #161b22;
      gap: 8px;
      align-items: center;
    }
    .ai-user-input {
      flex: 1;
      padding: 12px;
      border: none;
      border-radius: 8px;
      background: #0d1117;
      color: #fff;
      font-size: 16px;
    }
    .ai-send-btn {
      padding: 12px 16px;
      background: #58a6ff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      color: #fff;
      font-size: 16px;
    }
    .ai-msg-time {
      font-size: 11px;
      opacity: 0.7;
      text-align: left;
      margin-top: 4px;
    }
    .frame-1 {
      border: 15px solid #3b82f6;
      border-radius: 5px;
    }
    .frame-2 {
      border: 10px dashed #f59e0b;
    }
    .frame-3 {
      border: 20px double #10b981;
    }
    .frame-4 {
      border: 5px solid #8b5cf6;
      box-shadow: 0 0 20px rgba(139, 92, 246, 0.5);
    }
    .frame-5 {
      border-top: 10px solid #ef4444;
      border-bottom: 10px solid #ef4444;
      background: linear-gradient(to right, rgba(239, 68, 68, 0.1), rgba(239, 68, 68, 0.3));
    }
    .text-effect-1 {
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    }
    .text-effect-2 {
      background: linear-gradient(to right, #f97316, #f43f5e);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
    }
    .text-effect-3 {
      letter-spacing: 2px;
      font-weight: bold;
    }
    .text-effect-4 {
      text-shadow: 0 0 10px rgba(255, 255, 255, 0.8), 0 0 20px rgba(255, 255, 255, 0.5);
    }
    .banner-preview {
      transition: all 0.3s ease;
    }
    .control-group {
      background: #f8fafc;
      border-radius: 10px;
      padding: 15px;
      margin-bottom: 15px;
    }
    .control-label {
      display: block;
      font-weight: 600;
      margin-bottom: 8px;
      color: #334155;
    }
    .btn-primary {
      background: #3b82f6;
      color: white;
      border: none;
      border-radius: 8px;
      padding: 12px 20px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }
    .btn-primary:hover {
      background: #2563eb;
      transform: translateY(-2px);
      box-shadow: 0 4px 6px rgba(37, 99, 235, 0.3);
    }
    .gallery-item {
      transition: all 0.3s;
      cursor: pointer;
    }
    .gallery-item:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
    }
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @media (max-width: 768px) {
      .container {
        padding: 10px;
      }
      .tabs-container {
        padding: 8px;
      }
      .tab {
        padding: 10px 15px;
        font-size: 14px;
      }
      .page {
        padding: 15px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- هدر -->
    <div class="header">
      <h1 class="text-2xl font-bold text-center text-blue-600">
        <i class="fas fa-image ml-2"></i>بنر ساز حرفه‌ای
      </h1>
      <p class="text-center text-gray-600 mt-2">ساخت بنرهای زیبا و حرفه‌ای در کمتر از چند دقیقه</p>
    </div>

    <!-- تب‌های صفحه -->
    <div class="tabs-container">
      <div class="tab active" data-page="design">
        <i class="fas fa-paint-brush"></i>
        <span>طراحی بنر</span>
      </div>
      <div class="tab" data-page="frames">
        <i class="fas fa-border-all"></i>
        <span>قاب‌ها</span>
      </div>
      <div class="tab" data-page="effects">
        <i class="fas fa-magic"></i>
        <span>افکت‌ها</span>
      </div>
      <div class="tab" data-page="gallery">
        <i class="fas fa-images"></i>
        <span>گالری</span>
      </div>
      <div class="tab" data-page="saved">
        <i class="fas fa-save"></i>
        <span>ذخیره شده‌ها</span>
      </div>
      <div class="tab" id="ai-tab-btn">
        <i class="fas fa-robot"></i>
        <span>هوش مصنوعی</span>
      </div>
    </div>

    <!-- صفحه طراحی بنر -->
    <div class="page active" id="design-page">
      <h2 class="text-xl font-bold text-gray-800 mb-4">
        <i class="fas fa-sliders-h ml-2"></i>تنظیمات بنر
      </h2>
      
      <div class="grid grid-cols-1 md:grid-cols-2 gap-5">
        <div class="control-group">
          <label class="control-label">متن بنر</label>
          <input id="bannerText" type="text" class="w-full p-3 border rounded-lg" placeholder="متن خود را وارد کنید" value="بنر نمونه">
        </div>
        <div class="control-group">
          <label class="control-label">رنگ پس‌زمینه</label>
          <input id="bgColor" type="color" class="w-full h-12 border rounded-lg" value="#2563eb">
        </div>
        <div class="control-group">
          <label class="control-label">تصویر پس‌زمینه</label>
          <input id="bgImage" type="file" accept="image/*" class="w-full p-2 border rounded-lg">
        </div>
        <div class="control-group">
          <label class="control-label">رنگ متن</label>
          <input id="textColor" type="color" class="w-full h-12 border rounded-lg" value="#ffffff">
        </div>
        <div class="control-group">
          <label class="control-label">اندازه فونت</label>
          <div class="flex items-center mt-1">
            <input id="fontSize" type="range" min="10" max="100" value="24" class="w-full">
            <span id="fontSizeValue" class="mr-3 w-12 text-center">24px</span>
          </div>
        </div>
        <div class="control-group">
          <label class="control-label">نوع فونت</label>
          <select id="fontFamily" class="w-full p-3 border rounded-lg">
            <option value="Vazir">وزیر</option>
            <option value="Arial">Arial</option>
            <option value="Tahoma">Tahoma</option>
            <option value="Georgia">Georgia</option>
          </select>
        </div>
        <div class="control-group">
          <label class="control-label">اضافه کردن لوگو</label>
          <input id="logoImage" type="file" accept="image/*" class="w-full p-2 border rounded-lg">
        </div>
        <div class="control-group">
          <label class="control-label">تراز متن</label>
          <select id="textAlign" class="w-full p-3 border rounded-lg">
            <option value="center">وسط</option>
            <option value="right">راست</option>
            <option value="left">چپ</option>
          </select>
        </div>
      </div>

      <div class="mt-8">
        <h2 class="text-xl font-bold text-gray-800 mb-4">
          <i class="fas fa-eye ml-2"></i>پیش نمایش بنر
        </h2>
        <div id="bannerPreview" class="banner-preview w-full h-72 flex items-center justify-center text-center rounded-xl overflow-hidden relative" style="background-color: #2563eb; color: #ffffff; font-family: Vazir; font-size: 24px;">
          بنر نمونه
          <img id="logoPreview" class="absolute top-4 left-4 w-12 h-12 hidden" src="" alt="لوگو">
        </div>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mt-6">
          <button id="downloadBtn" class="btn-primary">
            <i class="fas fa-download ml-2"></i>دانلود بنر
          </button>
          <button id="saveBannerBtn" class="btn-primary">
            <i class="fas fa-save ml-2"></i>ذخیره بنر
          </button>
          <button id="resetBannerBtn" class="btn-primary" style="background: #ef4444;">
            <i class="fas fa-trash-alt ml-2"></i>بازنشانی
          </button>
        </div>
      </div>
    </div>

    <!-- صفحه قاب‌ها -->
    <div class="page" id="frames-page">
      <h2 class="text-xl font-bold text-gray-800 mb-6">
        <i class="fas fa-border-all ml-2"></i>انتخاب قاب
      </h2>
      <div class="grid grid-cols-2 md:grid-cols-3 gap-5">
        <div class="frame-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-frame="none">
          <div class="h-24 bg-gray-100 rounded flex items-center justify-center">بدون قاب</div>
          <p class="mt-2">بدون قاب</p>
        </div>
        <div class="frame-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-frame="frame-1">
          <div class="h-24 bg-gray-100 rounded frame-1 flex items-center justify-center">قاب 1</div>
          <p class="mt-2">قاب ساده</p>
        </div>
        <div class="frame-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-frame="frame-2">
          <div class="h-24 bg-gray-100 rounded frame-2 flex items-center justify-center">قاب 2</div>
          <p class="mt-2">قاب نقطه‌چین</p>
        </div>
        <div class="frame-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-frame="frame-3">
          <div class="h-24 bg-gray-100 rounded frame-3 flex items-center justify-center">قاب 3</div>
          <p class="mt-2">قاب دوبل</p>
        </div>
        <div class="frame-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-frame="frame-4">
          <div class="h-24 bg-gray-100 rounded frame-4 flex items-center justify-center">قاب 4</div>
          <p class="mt-2">قاب سایه‌دار</p>
        </div>
        <div class="frame-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-frame="frame-5">
          <div class="h-24 bg-gray-100 rounded frame-5 flex items-center justify-center">قاب 5</div>
          <p class="mt-2">قاب افقی</p>
        </div>
      </div>
    </div>

    <!-- صفحه افکت‌ها -->
    <div class="page" id="effects-page">
      <h2 class="text-xl font-bold text-gray-800 mb-6">
        <i class="fas fa-magic ml-2"></i>افکت‌های متنی
      </h2>
      <div class="grid grid-cols-2 md:grid-cols-4 gap-5">
        <div class="effect-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-effect="none">
          <div class="h-20 bg-gray-100 rounded flex items-center justify-center">بدون افکت</div>
          <p class="mt-2">بدون افکت</p>
        </div>
        <div class="effect-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-effect="text-effect-1">
          <div class="h-20 bg-gray-100 rounded flex items-center justify-center text-effect-1">سایه دار</div>
          <p class="mt-2">سایه دار</p>
        </div>
        <div class="effect-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-effect="text-effect-2">
          <div class="h-20 bg-gray-100 rounded flex items-center justify-center text-effect-2">گرادینت</div>
          <p class="mt-2">گرادینت</p>
        </div>
        <div class="effect-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-effect="text-effect-3">
          <div class="h-20 bg-gray-100 rounded flex items-center justify-center text-effect-3">ضخیم</div>
          <p class="mt-2">ضخیم</p>
        </div>
        <div class="effect-option border-2 border-gray-200 p-3 rounded-lg cursor-pointer text-center" data-effect="text-effect-4">
          <div class="h-20 bg-gray-100 rounded flex items-center justify-center text-effect-4">نئون</div>
          <p class="mt-2">نئون</p>
        </div>
      </div>
    </div>

    <!-- صفحه گالری -->
    <div class="page" id="gallery-page">
      <h2 class="text-xl font-bold text-gray-800 mb-6">
        <i class="fas fa-images ml-2"></i>گالری بنرهای آماده
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div class="gallery-item bg-blue-100 p-4 rounded-lg" data-banner="banner1">
          <div class="h-40 bg-blue-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
            بنر تبلیغاتی
          </div>
          <p class="text-center mt-3 font-medium">بنر آبی ساده</p>
        </div>
        <div class="gallery-item bg-red-100 p-4 rounded-lg" data-banner="banner2">
          <div class="h-40 bg-red-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
            تخفیف ویژه
          </div>
          <p class="text-center mt-3 font-medium">بنر قرمز تخفیف</p>
        </div>
        <div class="gallery-item bg-green-100 p-4 rounded-lg" data-banner="banner3">
          <div class="h-40 bg-green-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
            جدیدترین محصولات
          </div>
          <p class="text-center mt-3 font-medium">بنر سبز محصولات</p>
        </div>
        <div class="gallery-item bg-purple-100 p-4 rounded-lg" data-banner="banner4">
          <div class="h-40 bg-purple-500 rounded-lg flex items-center justify-center text-white text-xl font-bold">
            رویداد ویژه
          </div>
          <p class="text-center mt-3 font-medium">بنر بنفش رویداد</p>
        </div>
      </div>
    </div>

    <!-- صفحه ذخیره شده‌ها -->
    <div class="page" id="saved-page">
      <h2 class="text-xl font-bold text-gray-800 mb-6">
        <i class="fas fa-save ml-2"></i>بنرهای ذخیره شده شما
      </h2>
      <div id="userBannersList" class="grid grid-cols-1 md:grid-cols-2 gap-5">
        <p class="text-gray-500 text-center py-8">هیچ بنری ذخیره نکرده‌اید</p>
      </div>
    </div>
  </div>

  <!-- بخش هوش مصنوعی تمام صفحه -->
  <div class="ai-fullscreen" id="ai-fullscreen">
    <div class="ai-header">
      <h2 class="text-xl font-bold text-white">🤖 چت هوش مصنوعی</h2>
      <button class="ai-close" id="ai-close">
        <i class="fas fa-times ml-2"></i>بستن
      </button>
    </div>
    <div class="ai-content">
      <div class="ai-chat-container">
        <div id="ai-chatWindow" class="ai-chat-window"></div>
        <div class="ai-input-area">
          <input type="text" id="ai-userInput" class="ai-user-input" placeholder="پیام خود را بنویسید...">
          <button id="ai-sendBtn" class="ai-send-btn">
            <i class="fas fa-paper-plane ml-2"></i>ارسال
          </button>
        </div>
      </div>
    </div>
  </div>

  <script>
    // عناصر DOM
    const bannerText = document.getElementById('bannerText');
    const bgColor = document.getElementById('bgColor');
    const bgImage = document.getElementById('bgImage');
    const textColor = document.getElementById('textColor');
    const fontSize = document.getElementById('fontSize');
    const fontSizeValue = document.getElementById('fontSizeValue');
    const fontFamily = document.getElementById('fontFamily');
    const textAlign = document.getElementById('textAlign');
    const logoImage = document.getElementById('logoImage');
    const bannerPreview = document.getElementById('bannerPreview');
    const logoPreview = document.getElementById('logoPreview');
    const downloadBtn = document.getElementById('downloadBtn');
    const saveBannerBtn = document.getElementById('saveBannerBtn');
    const resetBannerBtn = document.getElementById('resetBannerBtn');
    const tabs = document.querySelectorAll('.tab');
    const pages = document.querySelectorAll('.page');
    const frameOptions = document.querySelectorAll('.frame-option');
    const effectOptions = document.querySelectorAll('.effect-option');
    const galleryItems = document.querySelectorAll('.gallery-item');
    const userBannersList = document.getElementById('userBannersList');
    const aiTabBtn = document.getElementById('ai-tab-btn');
    const aiFullscreen = document.getElementById('ai-fullscreen');
    const aiClose = document.getElementById('ai-close');
    const aiChatWindow = document.getElementById('ai-chatWindow');
    const aiUserInput = document.getElementById('ai-userInput');
    const aiSendBtn = document.getElementById('ai-sendBtn');

    // مقداردهی اولیه
    let currentFrame = 'none';
    let currentEffect = 'none';
    let userBanners = JSON.parse(localStorage.getItem('userBanners')) || [];
    let selectedModel = "openai-large";

    // نمایش اندازه فونت
    fontSizeValue.textContent = `${fontSize.value}px`;

    // تغییر صفحات
    tabs.forEach(tab => {
      tab.addEventListener('click', () => {
        if (tab.id === 'ai-tab-btn') {
          // نمایش بخش هوش مصنوعی در حالت تمام صفحه
          aiFullscreen.classList.add('active');
          return;
        }
        
        const pageId = `${tab.dataset.page}-page`;
        
        // غیرفعال کردن همه تب‌ها و صفحات
        tabs.forEach(t => t.classList.remove('active'));
        pages.forEach(page => page.classList.remove('active'));
        
        // فعال کردن تب و صفحه انتخاب شده
        tab.classList.add('active');
        document.getElementById(pageId).classList.add('active');
      });
    });

    // بستن بخش هوش مصنوعی
    aiClose.addEventListener('click', () => {
      aiFullscreen.classList.remove('active');
    });

    // به روزرسانی بنر
    function updateBanner() {
      bannerPreview.textContent = bannerText.value;
      bannerPreview.style.backgroundColor = bgColor.value;
      bannerPreview.style.color = textColor.value;
      bannerPreview.style.fontSize = `${fontSize.value}px`;
      bannerPreview.style.fontFamily = fontFamily.value;
      bannerPreview.style.textAlign = textAlign.value;
      
      // اعمال قاب انتخاب شده
      frameOptions.forEach(option => {
        bannerPreview.classList.remove(option.dataset.frame);
      });
      if (currentFrame !== 'none') {
        bannerPreview.classList.add(currentFrame);
      }
      
      // اعمال افکت انتخاب شده
      effectOptions.forEach(option => {
        bannerPreview.classList.remove(option.dataset.effect);
      });
      if (currentEffect !== 'none') {
        bannerPreview.classList.add(currentEffect);
      }
    }

    // انتخاب قاب
    frameOptions.forEach(option => {
      option.addEventListener('click', () => {
        currentFrame = option.dataset.frame;
        updateBanner();
      });
    });

    // انتخاب افکت
    effectOptions.forEach(option => {
      option.addEventListener('click', () => {
        currentEffect = option.dataset.effect;
        updateBanner();
      });
    });

    // رویدادهای ورودی
    bannerText.addEventListener('input', updateBanner);
    bgColor.addEventListener('input', updateBanner);
    textColor.addEventListener('input', updateBanner);
    fontSize.addEventListener('input', () => {
      fontSizeValue.textContent = `${fontSize.value}px`;
      updateBanner();
    });
    fontFamily.addEventListener('change', updateBanner);
    textAlign.addEventListener('change', updateBanner);

    bgImage.addEventListener('change', function () {
      const file = bgImage.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function (e) {
          bannerPreview.style.backgroundImage = `url('${e.target.result}')`;
        };
        reader.readAsDataURL(file);
      } else {
        bannerPreview.style.backgroundImage = '';
      }
    });

    logoImage.addEventListener('change', function () {
      const file = logoImage.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function (e) {
          logoPreview.src = e.target.result;
          logoPreview.classList.remove('hidden');
        };
        reader.readAsDataURL(file);
      } else {
        logoPreview.src = '';
        logoPreview.classList.add('hidden');
      }
    });

    // دانلود بنر
    downloadBtn.addEventListener('click', function () {
      html2canvas(bannerPreview).then(canvas => {
        const link = document.createElement('a');
        link.download = 'banner.png';
        link.href = canvas.toDataURL('image/png');
        link.click();
      });
    });

    // ذخیره بنر
    saveBannerBtn.addEventListener('click', function() {
      const bannerData = {
        text: bannerText.value,
        bgColor: bgColor.value,
        textColor: textColor.value,
        fontSize: fontSize.value,
        fontFamily: fontFamily.value,
        textAlign: textAlign.value,
        frame: currentFrame,
        effect: currentEffect,
        bgImage: bannerPreview.style.backgroundImage || '',
        logo: logoPreview.src || '',
        timestamp: new Date().toLocaleString('fa-IR')
      };
      
      userBanners.push(bannerData);
      localStorage.setItem('userBanners', JSON.stringify(userBanners));
      alert('بنر با موفقیت ذخیره شد!');
      updateUserBannersList();
    });

    // بارگذاری بنرهای ذخیره شده
    function updateUserBannersList() {
      if (userBanners.length === 0) {
        userBannersList.innerHTML = '<p class="text-gray-500 text-center py-8">هیچ بنری ذخیره نکرده‌اید</p>';
        return;
      }
      
      userBannersList.innerHTML = '';
      userBanners.forEach((banner, index) => {
        const bannerEl = document.createElement('div');
        bannerEl.className = 'gallery-item bg-gray-100 p-4 rounded-lg';
        bannerEl.innerHTML = `
          <div class="h-40 rounded-lg flex items-center justify-center text-white text-xl font-bold" style="background-color: ${banner.bgColor}; color: ${banner.textColor}; font-family: ${banner.fontFamily}; font-size: ${banner.fontSize}px; text-align: ${banner.textAlign}; background-image: ${banner.bgImage}">
            ${banner.text}
            ${banner.logo ? `<img src="${banner.logo}" class="absolute top-2 left-2 w-10 h-10">` : ''}
          </div>
          <p class="text-center mt-3 font-medium">ذخیره شده در: ${banner.timestamp}</p>
          <div class="flex gap-2 mt-3">
            <button class="load-banner-btn bg-blue-500 text-white p-2 rounded flex-1" data-index="${index}">بارگذاری</button>
            <button class="delete-banner-btn bg-red-500 text-white p-2 rounded flex-1" data-index="${index}">حذف</button>
          </div>
        `;
        userBannersList.appendChild(bannerEl);
      });
      
      // اضافه کردن رویداد به دکمه‌های بارگذاری و حذف
      document.querySelectorAll('.load-banner-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const index = e.target.dataset.index;
          loadBanner(userBanners[index]);
        });
      });
      
      document.querySelectorAll('.delete-banner-btn').forEach(btn => {
        btn.addEventListener('click', (e) => {
          const index = e.target.dataset.index;
          userBanners.splice(index, 1);
          localStorage.setItem('userBanners', JSON.stringify(userBanners));
          updateUserBannersList();
        });
      });
    }

    // بارگذاری بنر
    function loadBanner(bannerData) {
      bannerText.value = bannerData.text;
      bgColor.value = bannerData.bgColor;
      textColor.value = bannerData.textColor;
      fontSize.value = bannerData.fontSize;
      fontSizeValue.textContent = `${bannerData.fontSize}px`;
      fontFamily.value = bannerData.fontFamily;
      textAlign.value = bannerData.textAlign;
      currentFrame = bannerData.frame;
      currentEffect = bannerData.effect;
      bannerPreview.style.backgroundImage = bannerData.bgImage;
      
      if (bannerData.logo) {
        logoPreview.src = bannerData.logo;
        logoPreview.classList.remove('hidden');
      } else {
        logoPreview.src = '';
        logoPreview.classList.add('hidden');
      }
      
      updateBanner();
      alert('بنر با موفقیت بارگذاری شد!');
      
      // تغییر به صفحه طراحی
      tabs.forEach(t => t.classList.remove('active'));
      pages.forEach(p => p.classList.remove('active'));
      document.querySelector('[data-page="design"]').classList.add('active');
      document.getElementById('design-page').classList.add('active');
    }

    // بارگذاری بنرهای آماده
    galleryItems.forEach(item => {
      item.addEventListener('click', () => {
        const bannerType = item.dataset.banner;
        let bannerData = {};
        
        switch(bannerType) {
          case 'banner1':
            bannerData = {
              text: 'بنر تبلیغاتی',
              bgColor: '#3b82f6',
              textColor: '#ffffff',
              fontSize: 28,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-1',
              effect: 'text-effect-1'
            };
            break;
          case 'banner2':
            bannerData = {
              text: 'تخفیف ویژه',
              bgColor: '#ef4444',
              textColor: '#ffffff',
              fontSize: 32,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-2',
              effect: 'text-effect-3'
            };
            break;
          case 'banner3':
            bannerData = {
              text: 'جدیدترین محصولات',
              bgColor: '#10b981',
              textColor: '#ffffff',
              fontSize: 26,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-4',
              effect: 'text-effect-4'
            };
            break;
          case 'banner4':
            bannerData = {
              text: 'رویداد ویژه',
              bgColor: '#8b5cf6',
              textColor: '#ffffff',
              fontSize: 30,
              fontFamily: 'Vazir',
              textAlign: 'center',
              frame: 'frame-3',
              effect: 'text-effect-2'
            };
            break;
        }
        
        loadBanner(bannerData);
      });
    });

    // بازنشانی بنر
    resetBannerBtn.addEventListener('click', function() {
      if (confirm('آیا از بازنشانی بنر اطمینان دارید؟')) {
        bannerText.value = 'بنر نمونه';
        bgColor.value = '#2563eb';
        textColor.value = '#ffffff';
        fontSize.value = 24;
        fontSizeValue.textContent = '24px';
        fontFamily.value = 'Vazir';
        textAlign.value = 'center';
        bgImage.value = '';
        logoImage.value = '';
        bannerPreview.style.backgroundImage = '';
        logoPreview.src = '';
        logoPreview.classList.add('hidden');
        currentFrame = 'none';
        currentEffect = 'none';
        
        // حذف کلاس‌های قاب و افکت
        frameOptions.forEach(option => {
          bannerPreview.classList.remove(option.dataset.frame);
        });
        effectOptions.forEach(option => {
          bannerPreview.classList.remove(option.dataset.effect);
        });
        
        updateBanner();
      }
    });

    // ==================== بخش هوش مصنوعی ====================

    // افزودن پیام به چت
    function addAIMessage(text, sender, isTyping = false) {
      const msgDiv = document.createElement("div");
      msgDiv.className = `ai-message ${sender === "user" ? "ai-user" : "ai-bot"}`;
      
      const time = new Date().toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'});
      
      msgDiv.innerHTML = `
        <span>${text}</span>
        <div class="ai-msg-time">${time}</div>
      `;
      
      if (isTyping) msgDiv.classList.add("ai-typing");
      aiChatWindow.appendChild(msgDiv);
      aiChatWindow.scrollTop = aiChatWindow.scrollHeight;
      
      return msgDiv;
    }

    // ارسال پیام به هوش مصنوعی
    async function sendAIMessage() {
      const text = aiUserInput.value.trim();
      if (!text) return;
      
      addAIMessage(text, "user");
      aiUserInput.value = "";

      const loadingMsg = addAIMessage("در حال دریافت پاسخ...", "bot", true);

      try {
        // استفاده از API هوش مصنوعی
        const response = await fetch(`https://api2.api-code.ir/gpt-save-v2/?model=${selectedModel}&userid=mahdi&prompt=${encodeURIComponent(text)}`);
        const data = await response.text();
        loadingMsg.remove();
        addAIMessage(data, "bot");
      } catch(err) {
        loadingMsg.remove();
        addAIMessage("❌ خطا در دریافت پاسخ. لطفا دوباره تلاش کنید.", "bot");
        console.error(err);
      }
    }

    // رویدادهای بخش هوش مصنوعی
    aiSendBtn.addEventListener("click", sendAIMessage);
    aiUserInput.addEventListener("keydown", (e) => {
      if (e.key === "Enter") sendAIMessage();
    });

    // مقداردهی اولیه
    window.addEventListener('DOMContentLoaded', () => {
      updateBanner();
      updateUserBannersList();
      
      // اضافه کردن پیام خوشامدگویی به چت هوش مصنوعی
      addAIMessage("سلام! من هوش مصنوعی هستم که می‌توانم به شما در طراحی بنر کمک کنم. چه سوالی دارید؟", "bot");
    });
  </script>
</body>
</html>
