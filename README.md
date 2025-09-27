    }

    .display {<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>পবিত্র বাইবেল</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            background-color: #000;
            display: flex;
            justify-content: center;
        }

        .app-container {
            width: 100%;
            max-width: 450px; /* মোবাইল ফ্রেমের প্রস্থ */
            min-height: 100vh;
            background-color: #121212; /* প্রধান কালো ব্যাকগ্রাউন্ড */
            color: #e0e0e0;
            position: relative;
            overflow: hidden;
        }

        .screen {
            height: 100vh;
            position: absolute;
            width: 100%;
            top: 0;
            transition: transform 0.3s ease-in-out;
            box-sizing: border-box;
            padding-top: 60px; /* হেডারের উচ্চতা */
        }

        .hidden {
            display: none !important;
        }

        /* --- হেডার স্টাইল --- */
        .header {
            background-color: #0b7af0; /* নীল হেডার */
            padding: 15px 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            color: white;
            font-size: 18px;
            position: fixed; /* হেডার স্ক্রল হবে না */
            width: inherit;
            max-width: 450px;
            top: 0;
            z-index: 10;
        }

        .header i, .floating-action-button {
            cursor: pointer;
        }

        /* --- বুক লিস্ট --- */
        .book-list-content {
            overflow-y: auto;
            height: calc(100% - 60px); 
        }
        
        .book-list-heading {
            padding: 10px 15px;
            background-color: #333; 
            color: #0b7af0; 
            font-weight: bold;
            font-size: 14px;
            margin-top: 0;
            border-top: 1px solid #444;
        }

        .book-item {
            padding: 15px;
            border-bottom: 1px solid #333;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.1s;
        }
        
        .book-item:hover {
            background-color: #222;
        }

        .floating-action-button {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #e91e63; /* গোলাপি রং */
            color: white;
            border-radius: 50%;
            width: 56px;
            height: 56px;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 24px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.4);
            z-index: 15;
        }
        .app-container > .floating-action-button {
            right: calc(50% - 450px/2 + 20px); 
        }
        @media (max-width: 450px) {
            .app-container > .floating-action-button {
                right: 20px;
            }
        }


        /* --- রিডিং স্ক্রিন --- */
        .chapter-content {
            padding: 15px;
            padding-bottom: 70px; /* ফুটারে স্পেস */
            overflow-y: auto;
            height: calc(100% - 60px);
        }

        .verse {
            line-height: 1.6;
            margin-bottom: 10px;
            text-align: justify; /* পাঠযোগ্যতা বাড়াতে */
        }

        .verse-number {
            font-weight: bold;
            color: #0b7af0;
            margin-right: 8px;
        }

        /* --- ফুটার নেভিগেশন --- */
        .footer-nav {
            position: fixed;
            bottom: 0;
            width: 100%;
            max-width: 450px;
            background-color: #1a1a1a;
            display: flex;
            justify-content: flex-start; /* বাম দিক থেকে শুরু */
            overflow-x: auto; /* ফুটারে স্ক্রল করার সুবিধা */
            padding: 10px;
            z-index: 11;
        }
        /* ফুটারে স্ক্রলবার লুকিয়ে রাখা */
        .footer-nav::-webkit-scrollbar {
            display: none;
        }
        .footer-nav {
            -ms-overflow-style: none; /* IE and Edge */
            scrollbar-width: none;  /* Firefox */
        }


        .footer-nav span {
            color: #fff;
            padding: 5px 12px;
            margin: 0 4px;
            flex-shrink: 0; /* যেন সংখ্যাগুলো ছোট না হয় */
            border-radius: 4px;
            cursor: pointer;
        }

        .footer-nav .active {
            background-color: #e91e63; /* অ্যাকটিভ চ্যাপ্টার গোলাপি */
        }

        /* --- মেনু/সাইডবার স্টাইল --- */
        .side-menu {
            position: fixed;
            top: 0;
            left: 0;
            width: 75%;
            height: 100%;
            background-color: #2c2c2c;
            z-index: 20;
            transform: translateX(-100%); 
            transition: transform 0.3s ease-in-out;
            padding-top: 0;
        }

        .side-menu.active {
            transform: translateX(0); 
        }

        .menu-header {
            background-color: #0b7af0;
            color: white;
            padding: 20px 15px;
            font-size: 20px;
            font-weight: bold;
        }

        .menu-item {
            padding: 15px;
            border-bottom: 1px solid #444;
            font-size: 16px;
            cursor: pointer;
        }
        
        .menu-item i {
            margin-right: 10px;
            color: #0b7af0;
        }

        /* --- মডাল/অনুসন্ধান ও ব্রাউজ স্টাইল --- */
        .modal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 30;
        }

        .modal-content {
            background-color: #333;
            padding: 20px;
            border-radius: 8px;
            width: 80%;
            max-width: 350px;
            color: white;
            text-align: center;
        }

        .modal-actions {
            display: flex;
            justify-content: flex-end;
            margin-top: 15px;
        }

        .modal-actions button {
            background: none;
            border: none;
            color: #0b7af0;
            padding: 10px;
            font-weight: bold;
            cursor: pointer;
            margin-left: 10px;
        }
        input, select {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            background-color: #444;
            border: 1px solid #555;
            color: white;
            border-radius: 4px;
            box-sizing: border-box;
        }
        
        .select-options select {
            margin-bottom: 5px;
        }
    </style>
</head>
<body>

<div class="app-container">
    
    <div id="bookListScreen" class="screen">
        <header class="header">
            <i class="fas fa-bars menu-icon" onclick="toggleMenu()"></i>
            <span class="header-title">পবিত্র বাইবেল</span>
            <i class="fas fa-cog settings-icon"></i>
        </header>
        <div id="book-list" class="book-list-content">
            
            <div class="book-list-heading">পুরাতন নিয়ম (Old Testament)</div>
            <div class="book-item" onclick="openChapter('আদিপুস্তক')">আদিপুস্তক (Genesis)</div>
            <div class="book-item" onclick="openChapter('যাত্রা পুস্তক')">যাত্রা পুস্তক (Exodus)</div>
            <div class="book-item" onclick="openChapter('লেবীয় পুস্তক')">লেবীয় পুস্তক (Leviticus)</div>
            <div class="book-item" onclick="openChapter('গণনা পুস্তক')">গণনা পুস্তক (Numbers)</div>
            <div class="book-item" onclick="openChapter('দ্বিতীয় বিবরণ')">দ্বিতীয় বিবরণ (Deuteronomy)</div>
            <div class="book-item" onclick="openChapter('যোশুয়া')">যোশুয়া (Joshua)</div>
            <div class="book-item" onclick="openChapter('বিচারকর্তৃগণ')">বিচারকর্তৃগণ (Judges)</div>
            <div class="book-item" onclick="openChapter('রূথ')">রূথ (Ruth)</div>
            <div class="book-item" onclick="openChapter('১ শমূয়েল')">১ শমূয়েল (1 Samuel)</div>
            <div class="book-item" onclick="openChapter('২ শমূয়েল')">২ শমূয়েল (2 Samuel)</div>
            <div class="book-item" onclick="openChapter('১ রাজাবলি')">১ রাজাবলি (1 Kings)</div>
            <div class="book-item" onclick="openChapter('২ রাজাবলি')">২ রাজাবলি (2 Kings)</div>
            <div class="book-item" onclick="openChapter('১ বংশাবলি')">১ বংশাবলি (1 Chronicles)</div>
            <div class="book-item" onclick="openChapter('২ বংশাবলি')">২ বংশাবলি (2 Chronicles)</div>
            <div class="book-item" onclick="openChapter('এস্রা')">এস্রা (Ezra)</div>
            <div class="book-item" onclick="openChapter('নহমিয়')">নহমিয় (Nehemiah)</div>
            <div class="book-item" onclick="openChapter('এষ্ঠের')">এষ্ঠের (Esther)</div>
            <div class="book-item" onclick="openChapter('ইয়োব')">ইয়োব (Job)</div>
            <div class="book-item" onclick="openChapter('গীতসংহিতা')">গীতসংহিতা (Psalms)</div>
            <div class="book-item" onclick="openChapter('হিতোপদেশ')">হিতোপদেশ (Proverbs)</div>
            <div class="book-item" onclick="openChapter('উপদেশক')">উপদেশক (Ecclesiastes)</div>
            <div class="book-item" onclick="openChapter('পরমগীত')">পরমগীত (Song of Solomon)</div>
            <div class="book-item" onclick="openChapter('যিশাইয়')">যিশাইয় (Isaiah)</div>
            <div class="book-item" onclick="openChapter('যিরমিয়')">যিরমিয় (Jeremiah)</div>
            <div class="book-item" onclick="openChapter('বিলাপ')">বিলাপ (Lamentations)</div>
            <div class="book-item" onclick="openChapter('যিহিষ্কেল')">যিহিষ্কেল (Ezekiel)</div>
            <div class="book-item" onclick="openChapter('দানিয়েল')">দানিয়েল (Daniel)</div>
            <div class="book-item" onclick="openChapter('হোশেয়')">হোশেয় (Hosea)</div>
            <div class="book-item" onclick="openChapter('যোয়েল')">যোয়েল (Joel)</div>
            <div class="book-item" onclick="openChapter('আমোস')">আমোস (Amos)</div>
            <div class="book-item" onclick="openChapter('ওবদিয়')">ওবদিয় (Obadiah)</div>
            <div class="book-item" onclick="openChapter('যোনা')">যোনা (Jonah)</div>
            <div class="book-item" onclick="openChapter('মীখা')">মীখা (Micah)</div>
            <div class="book-item" onclick="openChapter('নাহূম')">নাহূম (Nahum)</div>
            <div class="book-item" onclick="openChapter('হבק্‌কূক')">হבק্‌কূক (Habakkuk)</div>
            <div class="book-item" onclick="openChapter('সেফনিয়')">সেফনিয় (Zephaniah)</div>
            <div class="book-item" onclick="openChapter('হগয়')">হগয় (Haggai)</div>
            <div class="book-item" onclick="openChapter('সখরিয়')">সখরিয় (Zechariah)</div>
            <div class="book-item" onclick="openChapter('মালাখি')">মালাখি (Malachi)</div>

            <div class="book-list-heading">নতুন নিয়ম (New Testament)</div>
            <div class="book-item" onclick="openChapter('মথি')">মথি (Matthew)</div>
            <div class="book-item" onclick="openChapter('মার্ক')">মার্ক (Mark)</div>
            <div class="book-item" onclick="openChapter('লূক')">লূক (Luke)</div>
            <div class="book-item" onclick="openChapter('যোহন')">যোহন (John)</div>
            <div class="book-item" onclick="openChapter('প্রেরিত')">প্রেরিত (Acts)</div>
            <div class="book-item" onclick="openChapter('রোমীয়')">রোমীয় (Romans)</div>
            <div class="book-item" onclick="openChapter('১ করিন্থীয়')">১ করিন্থীয় (1 Corinthians)</div>
            <div class="book-item" onclick="openChapter('২ করিন্থীয়')">২ করিন্থীয় (2 Corinthians)</div>
            <div class="book-item" onclick="openChapter('গালাতীয়')">গালাতীয় (Galatians)</div>
            <div class="book-item" onclick="openChapter('ইফিষীয়')">ইফিষীয় (Ephesians)</div>
            <div class="book-item" onclick="openChapter('ফিলিপীয়')">ফিলিপীয় (Philippians)</div>
            <div class="book-item" onclick="openChapter('কলসীয়')">কলসীয় (Colossians)</div>
            <div class="book-item" onclick="openChapter('১ থিষলনীকীয়')">১ থিষলনীকীয় (1 Thessalonians)</div>
            <div class="book-item" onclick="openChapter('২ থিষলনীকীয়')">২ থিষলনীকীয় (2 Thessalonians)</div>
            <div class="book-item" onclick="openChapter('১ তীমথিয়')">১ তীমথিয় (1 Timothy)</div>
            <div class="book-item" onclick="openChapter('২ তীমথিয়')">২ তীমথিয় (2 Timothy)</div>
            <div class="book-item" onclick="openChapter('তীত')">তীত (Titus)</div>
            <div class="book-item" onclick="openChapter('ফিলিমন')">ফিলিমন (Philemon)</div>
            <div class="book-item" onclick="openChapter('ইব্রীয়')">ইব্রীয় (Hebrews)</div>
            <div class="book-item" onclick="openChapter('যাকোব')">যাকোব (James)</div>
            <div class="book-item" onclick="openChapter('১ পিতর')">১ পিতর (1 Peter)</div>
            <div class="book-item" onclick="openChapter('২ পিতর')">২ পিতর (2 Peter)</div>
            <div class="book-item" onclick="openChapter('১ যোহন')">১ যোহন (1 John)</div>
            <div class="book-item" onclick="openChapter('২ যোহন')">২ যোহন (2 John)</div>
            <div class="book-item" onclick="openChapter('৩ যোহন')">৩ যোহন (3 John)</div>
            <div class="book-item" onclick="openChapter('যিহূদা')">যিহূদা (Jude)</div>
            <div class="book-item" onclick="openChapter('প্রকাশিত বাক্য')">প্রকাশিত বাক্য (Revelation)</div>
        </div>
        <div class="floating-action-button" onclick="openBrowseModal()">
            <i class="fas fa-book"></i>
        </div>
    </div>
    
    <div id="readingScreen" class="screen hidden">
        <header class="header reading-header">
            <i class="fas fa-arrow-left back-icon" onclick="showScreen('bookListScreen')"></i>
            <span id="current-book-chapter" class="header-title">আদিপুস্তক ১</span>
            <i class="fas fa-bookmark bookmark-icon"></i>
        </header>
        <div id="chapter-content" class="chapter-content">
            </div>
        <div id="chapter-nav-footer" class="footer-nav">
            <span class="chapter-number active">১</span>
            <span class="chapter-number">২</span>
        </div>
    </div>

    <div id="sideMenu" class="side-menu hidden">
        <div class="menu-header">পবিত্র বাইবেল</div>
        <div class="menu-item"><i class="fas fa-book"></i> পবিত্র বাইবেল</div>
        <div class="menu-item"><i class="fas fa-church"></i> পুরাতন নিয়ম</div>
        <div class="menu-item"><i class="fas fa-cross"></i> নতুন নিয়ম</div>
        <div class="menu-item" onclick="showSearchModal()"><i class="fas fa-search"></i> অনুসন্ধান (Search)</div>
        <div class="menu-item"><i class="fas fa-star"></i> পছন্দের তালিকা (Favourites)</div>
    </div>

    <div id="searchModal" class="modal hidden">
        <div class="modal-content">
            <h4>বাইবেল অনুসন্ধান (Bible Search)</h4>
            <div class="search-input-area">
                <input type="text" id="search-phrase" placeholder="অনুসন্ধানের শব্দ/বাক্য (Phrase to search)">
                <select id="search-scope">
                    <option value="full">সম্পূর্ণ বাইবেল (Full Bible)</option>
                    <option value="ot">পুরাতন নিয়ম</option>
                </select>
            </div>
            <div class="modal-actions">
                <button class="cancel-button" onclick="hideSearchModal()">CANCEL</button>
                <button class="search-button">SEARCH</button>
            </div>
        </div>
    </div>

    <div id="browseModal" class="modal hidden">
        <div class="modal-content">
            <h4>Select</h4>
            <div class="select-options">
                <select><option>পুরাতন নিয়ম</option></select>
                <select><option>আদিপুস্তক</option></select>
                <select><option>Chapter ১</option></select>
                <select><option>Verse ১</option></select>
            </div>
            <div class="modal-actions">
                <button class="cancel-button" onclick="hideBrowseModal()">CANCEL</button>
                <button class="open-button">OPEN</button>
            </div>
        </div>
    </div>

</div>

<script>
    // স্ক্রিন ও মডালগুলির আইডি
    const SCREENS = {
        bookListScreen: document.getElementById('bookListScreen'),
        readingScreen: document.getElementById('readingScreen')
    };
    const MODALS = {
        sideMenu: document.getElementById('sideMenu'),
        searchModal: document.getElementById('searchModal'),
        browseModal: document.getElementById('browseModal')
    };

    // বাইবেলের সব বই এবং তাদের মোট অধ্যায় সংখ্যা 
    const BIBLE_CHAPTER_COUNT = {
        'আদিপুস্তক': 50, 'যাত্রা পুস্তক': 40, 'লেবীয় পুস্তক': 27, 'গণনা পুস্তক': 36, 'দ্বিতীয় বিবরণ': 34,
        'যোশুয়া': 24, 'বিচারকর্তৃগণ': 21, 'রূথ': 4, '১ শমূয়েল': 31, '২ শমূয়েল': 24,
        '১ রাজাবলি': 22, '২ রাজাবলি': 25, '১ বংশাবলি': 29, '২ বংশাবলি': 36, 'এস্রা': 10,
        'নহমিয়': 13, 'এষ্ঠের': 10, 'ইয়োব': 42, 'গীতসংহিতা': 150, 'হিতোপদেশ': 31,
        'উপদেশক': 12, 'পরমগীত': 8, 'যিশাইয়': 66, 'যিরমিয়': 52, 'বিলাপ': 5,
        'যিহিষ্কেল': 48, 'দানিয়েল': 12, 'হোশেয়': 14, 'যোয়েল': 3, 'আমোস': 9,
        'ওবদিয়': 1, 'যোনা': 4, 'মীখা': 7, 'নাহূম': 3, 'হבק্‌কূক': 3,
        'সেফনিয়': 3, 'হগয়': 2, 'সখরিয়': 14, 'মালাখি': 4,
        // নতুন নিয়ম
        'মথি': 28, 'মার্ক': 16, 'লূক': 24, 'যোহন': 21, 'প্রেরিত': 28,
        'রোমীয়': 16, '১ করিন্থীয়': 16, '২ করিন্থীয়': 13, 'গালাতীয়': 6, 'ইফিষীয়': 6,
        'ফিলিপীয়': 4, 'কলসীয়': 4, '১ থিষলনীকীয়': 5, '২ থিষলনীকীয়': 3, '১ তীমথিয়': 6,
        '২ তীমথিয়': 4, 'তীত': 3, 'ফিলিমন': 1, 'ইব্রীয়': 13, 'যাকোব': 5,
        '১ পিতর': 5, '২ পিতর': 3, '১ যোহন': 5, '২ যোহন': 1, '৩ যোহন': 1,
        'যিহূদা': 1, 'প্রকাশিত বাক্য': 22,
        'DEFAULT': 30 
    };

    // --- ⭐ বাইবেলের আসল পদ ডেটা (আদিপুস্তক ১-৫) ⭐ ---
    // বাকি পদগুলো এই ফরম্যাটে যোগ করতে হবে: "বইয়ের নাম": { "অধ্যায় সংখ্যা": { "পদ সংখ্যা": "পদের পাঠ্য", ... } }
    const BIBLE_TEXT_DATA = {
        "আদিপুস্তক": {
            "1": {
                "1": "আদিতে ঈশ্বর আকাশমণ্ডল ও পৃথিবীর সৃষ্টি করিলেন।",
                "2": "পৃথিবী ঘোর ও শূন্য ছিল, এবং অন্ধকার জলধির উপরে ছিল, আর ঈশ্বরের আত্মা জলের উপরে অবস্থিতি করিতেছিলেন।",
                "3": "পরে ঈশ্বর কহিলেন, দীপ্তি হউক; তাহাতে দীপ্তি হইল।",
                "4": "ঈশ্বর দেখিলেন যে, দীপ্তি উত্তম; তখন ঈশ্বর দীপ্তি হইতে অন্ধকার পৃথক করিলেন।",
                "5": "আর ঈশ্বর দীপ্তির নাম দিবস ও অন্ধকারের নাম রাত্রি রাখিলেন। এইরূপে সন্ধ্যা ও প্রভাত হইয়া প্রথম দিন হইল।",
                "6": "পরে ঈশ্বর কহিলেন, জলের মধ্যে বিতান হউক, এবং জলকে জল হইতে পৃথক করুক।",
                "7": "পরে ঈশ্বর বিতান নির্মাণ করিয়া বিতানের উর্দ্ধস্থ জল হইতে বিতানের অধঃস্থ জল পৃথক করিলেন; তাহাতে সেইরূপ হইল।",
                "8": "আর ঈশ্বর বিতানের নাম আকাশমণ্ডল রাখিলেন। এইরূপে সন্ধ্যা ও প্রভাত হইয়া দ্বিতীয় দিন হইল।",
                "9": "পরে ঈশ্বর কহিলেন, আকাশমণ্ডলের অধঃস্থ জল এক স্থানে সংগৃহীত হউক, ও স্থল দেখা যাক; তাহাতে সেইরূপ হইল।",
                "10": "আর ঈশ্বর স্থলের নাম পৃথিবী ও জলরাশির নাম সমুদ্র রাখিলেন; আর ঈশ্বর দেখিলেন যে, তাহা উত্তম।",
                "11": "পরে ঈশ্বর কহিলেন, ভূমি তৃণ, বীজোৎপাদক ওষধি, ও স্ব স্ব জাতি অনুযায়ী সবীজ ফলের উৎপাদক ফলবৃক্ষ, ভূমির উপরে উৎপন্ন করুক; তাহাতে সেইরূপ হইল।",
                "12": "ফলতঃ ভূমি তৃণ, স্ব স্ব জাতি অনুযায়ী বীজোৎপাদক ওষধি, ও স্ব স্ব জাতি অনুযায়ী সবীজ ফলের উৎপাদক বৃক্ষ, উৎপন্ন করিল; আর ঈশ্বর দেখিলেন যে, সে সকল উত্তম।",
                "13": "এইরূপে সন্ধ্যা ও প্রভাত হইয়া তৃতীয় দিন হইল।",
                "14": "পরে ঈশ্বর কহিলেন, দিবস হইতে রাত্রিকে পৃথক করিবার জন্য আকাশমণ্ডলের বিতানে জ্যোতির্গণ হউক; এবং তাহারা লক্ষণ নির্ণয় ও সময় সকল ও দিন ও বৎসর নিরূপণ করুক।",
                "15": "আর তাহারা পৃথিবীতে দীপ্তি দিবার জন্য আকাশমণ্ডলের বিতানে জ্যোতির্গণ হউক; তাহাতে সেইরূপ হইল।",
                "16": "পরে ঈশ্বর দ
      background-color: #000;
      color: #0f0;
      font-size: 32px;
      padding: 15px;
      border-radius: 8px;
      text-align: right;
      margin-bottom: 15px;
      height: 60px;
      overflow-x: auto;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      padding: 20px;
      font-size: 20px;
      border: none;
      border-radius: 10px;
      background-color: #333;
      color: #fff;
      cursor: pointer;
    }

    button:hover {
      background-color: #444;
    }

    .operator {
      background-color: #ffa500;
    }

    .clear {
      background-color: #e53935;
    }

    .equals {
      background-color: #00c853;
      grid-column: span 2;
    }
  </style>
</head>
<body>

  <!-- 🔝 Top Ad -->
  <div class="ad-slot">
    <script async="async" data-cfasync="false" src="//pl27108541.profitableratecpm.com/14f2186aede9c982aa64593ce37d869b/invoke.js"></script>
    <div id="container-14f2186aede9c982aa64593ce37d869b"></div>
  </div>

  <!-- 🔢 Calculator -->
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="clear" onclick="clearDisplay()">AC</button>
      <button onclick="append('%')">%</button>
      <button onclick="backspace()">⌫</button>
      <button class="operator" onclick="append('/')">÷</button>

      <button onclick="append('7')">7</button>
      <button onclick="append('8')">8</button>
      <button onclick="append('9')">9</button>
      <button class="operator" onclick="append('*')">×</button>

      <button onclick="append('4')">4</button>
      <button onclick="append('5')">5</button>
      <button onclick="append('6')">6</button>
      <button class="operator" onclick="append('-')">−</button>

      <button onclick="append('1')">1</button>
      <button onclick="append('2')">2</button>
      <button onclick="append('3')">3</button>
      <button class="operator" onclick="append('+')">+</button>

      <button onclick="append('00')">00</button>
      <button onclick="append('0')">0</button>
      <button onclick="append('.')">.</button>
      <button class="equals" onclick="calculate()">=</button>
    </div>
  </div>

  <!-- 🔻 Bottom Ad -->
  <div class="ad-slot">
    <script async="async" data-cfasync="false" src="//pl27108541.profitableratecpm.com/14f2186aede9c982aa64593ce37d869b/invoke.js"></script>
    <div id="container-14f2186aede9c982aa64593ce37d869b"></div>
  </div>

  <script>
    let display = document.getElementById('display');

    function append(char) {
      if (display.innerText === '0' && char !== '.') {
        display.innerText = char;
      } else {
        display.innerText += char;
      }
    }

    function clearDisplay() {
      display.innerText = '0';
    }

    function backspace() {
      display.innerText = display.innerText.slice(0, -1);
      if (display.innerText === '') {
        display.innerText = '0';
      }
    }

    function calculate() {
      try {
        let expression = display.innerText.replace(/÷/g, '/').replace(/×/g, '*');
        let result = eval(expression);
        display.innerText = result;
      } catch {
        display.innerText = 'Error';
      }
    }
  </script>
</body>
</html>
