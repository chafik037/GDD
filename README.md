<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>قالب GDD متكامل - مع Kanban ونظام حفظ</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* الوضع المظلم (Dark Mode) */
        body.light-mode {
            background: #e2e6e9;
        }

        body.dark-mode {
            background: #1a1a2e;
        }

        body.dark-mode .pdf-card {
            background: #1e1e2a;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.4);
        }

        body.dark-mode .doc-header {
            background: #0d0d1a;
            border-bottom-color: #e94560;
        }

        body.dark-mode .nav-tabs {
            background: #252536;
            border-bottom-color: #3a3a4a;
        }

        body.dark-mode .tab-btn {
            color: #c0c0e0;
        }

        body.dark-mode .tab-btn:hover {
            background: #35354a;
        }

        body.dark-mode .content-pane {
            background: #1e1e2a;
        }

        body.dark-mode h2, body.dark-mode h3 {
            color: #e0e0e0;
        }

        body.dark-mode table, body.dark-mode th, body.dark-mode td {
            border-color: #3a3a4a;
        }

        body.dark-mode th {
            background: #252536;
            color: #e0e0e0;
        }

        body.dark-mode .pillar-box {
            background: #252536;
        }

        body.dark-mode .footer-note {
            background: #0d0d1a;
            border-top-color: #3a3a4a;
            color: #888;
        }

        body.dark-mode .kanban-column {
            background: #252536;
        }

        body.dark-mode .kanban-card {
            background: #1e1e2a;
            border-left-color: #e94560;
        }

        body.dark-mode .setting-bar {
            background: #252536;
        }

        .setting-bar {
            background: #f4f6f9;
            padding: 10px 20px;
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            border-bottom: 1px solid #ddd;
        }

        .setting-btn {
            background: #1e2a3a;
            border: none;
            padding: 6px 15px;
            border-radius: 25px;
            color: white;
            cursor: pointer;
            font-family: inherit;
            font-size: 13px;
        }

        .setting-btn:hover {
            background: #e94560;
        }

        .theme-toggle {
            background: #2c3e50;
        }

        .save-status {
            font-size: 12px;
            color: #4caf50;
        }

        body.dark-mode .save-status {
            color: #80e080;
        }

        /* باقي الأنماط من القالب الأصلي */
        body {
            font-family: 'Segoe UI', 'Cairo', 'Tahoma', sans-serif;
            padding: 40px 20px;
            display: flex;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .pdf-card {
            max-width: 1400px;
            width: 100%;
            background: white;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
            border-radius: 4px;
            overflow: hidden;
            transition: all 0.3s ease;
        }

        .doc-header {
            background: #1e2a3a;
            color: white;
            padding: 25px 35px;
            border-bottom: 4px solid #e94560;
        }

        .doc-header h1 {
            font-size: 28px;
        }

        .doc-header .sub {
            color: #bbb;
            margin-top: 8px;
            font-size: 14px;
        }

        .meta-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            margin-top: 20px;
            font-size: 13px;
        }

        .meta-item {
            background: #0f1a24;
            padding: 6px 12px;
            border-radius: 20px;
        }

        .nav-tabs {
            display: flex;
            background: #f4f6f9;
            border-bottom: 1px solid #ddd;
            padding-right: 20px;
            flex-wrap: wrap;
        }

        .tab-btn {
            background: none;
            border: none;
            padding: 14px 18px;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: 0.2s;
            color: #1e2a3a;
            border-bottom: 3px solid transparent;
            font-family: inherit;
        }

        .tab-btn:hover {
            background: #e9ecef;
        }

        .tab-btn.active {
            border-bottom-color: #e94560;
            color: #e94560;
        }

        .content-pane {
            padding: 35px;
            background: white;
            min-height: 550px;
            transition: all 0.3s ease;
        }

        .tab-content {
            display: none;
            animation: fade 0.25s ease;
        }

        .tab-content.active-tab {
            display: block;
        }

        @keyframes fade {
            from { opacity: 0; transform: translateY(5px);}
            to { opacity: 1; transform: translateY(0);}
        }

        h2 {
            font-size: 22px;
            color: #1e2a3a;
            border-right: 5px solid #e94560;
            padding-right: 15px;
            margin-bottom: 20px;
        }

        h3 {
            margin: 20px 0 10px;
            color: #2c3e50;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            margin: 20px 0;
            font-size: 14px;
        }

        th, td {
            border: 1px solid #ccc;
            padding: 10px 12px;
            text-align: right;
            vertical-align: top;
        }

        th {
            background: #eef2f5;
            color: #1e2a3a;
        }

        .pillar-box {
            background: #f8f9fc;
            border-right: 4px solid #e94560;
            padding: 15px;
            margin: 15px 0;
            border-radius: 8px;
        }

        .code-block {
            background: #1e2a3a;
            color: #d4d4d4;
            padding: 15px;
            border-radius: 8px;
            font-family: monospace;
            font-size: 13px;
            overflow-x: auto;
            margin: 15px 0;
        }

        .footer-note {
            background: #f8f9fa;
            padding: 12px 20px;
            text-align: center;
            font-size: 12px;
            color: #6c757d;
            border-top: 1px solid #dee2e6;
        }

        button.action-print, .add-row-btn {
            background: #1e2a3a;
            border: none;
            color: white;
            padding: 8px 18px;
            border-radius: 30px;
            cursor: pointer;
            font-family: inherit;
            margin: 10px 10px 10px 0;
        }

        .add-row-btn {
            background: #27ae60;
            font-size: 12px;
        }

        .add-row-btn:hover {
            background: #2ecc71;
        }

        /* Kanban styles */
        .kanban-container {
            display: flex;
            gap: 20px;
            margin-top: 20px;
            flex-wrap: wrap;
        }

        .kanban-column {
            background: #f4f6f9;
            border-radius: 12px;
            flex: 1;
            min-width: 250px;
            padding: 15px;
        }

        .kanban-header {
            font-weight: bold;
            padding-bottom: 10px;
            margin-bottom: 15px;
            border-bottom: 2px solid #e94560;
            display: flex;
            justify-content: space-between;
        }

        .kanban-cards {
            min-height: 300px;
        }

        .kanban-card {
            background: white;
            border-right: 3px solid #e94560;
            padding: 12px;
            margin-bottom: 12px;
            border-radius: 8px;
            cursor: grab;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
            transition: 0.2s;
        }

        .kanban-card.dragging {
            opacity: 0.5;
            cursor: grabbing;
        }

        .kanban-card:hover {
            transform: translateX(-3px);
        }

        .card-title {
            font-weight: bold;
            margin-bottom: 6px;
        }

        .card-desc {
            font-size: 12px;
            color: #666;
        }

        .card-delete {
            float: left;
            cursor: pointer;
            color: #e94560;
            font-size: 12px;
        }

        .add-card-btn {
            width: 100%;
            background: none;
            border: 1px dashed #ccc;
            padding: 8px;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 10px;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            justify-content: center;
            align-items: center;
            z-index: 1000;
        }

        .modal-content {
            background: white;
            padding: 25px;
            border-radius: 12px;
            width: 400px;
            max-width: 90%;
        }

        body.dark-mode .modal-content {
            background: #2a2a3a;
            color: white;
        }

        .modal-content input, .modal-content textarea {
            width: 100%;
            padding: 8px;
            margin: 10px 0;
            border-radius: 6px;
            border: 1px solid #ccc;
        }

        .editable-field {
            background: #fffef7;
            border-left: 3px solid #e94560;
            padding: 8px 12px;
            margin: 10px 0;
        }

        body.dark-mode .editable-field {
            background: #2a2a3a;
        }

        @media print {
            body {
                background: white;
                padding: 0;
            }
            .nav-tabs, .action-print, .setting-bar, .add-row-btn, .add-card-btn, .card-delete, .theme-toggle, .save-status {
                display: none;
            }
            .tab-content {
                display: block !important;
            }
            .pdf-card {
                box-shadow: none;
            }
        }
    </style>
</head>
<body class="light-mode">
<div class="pdf-card" id="gddDocument">
    <div class="doc-header">
        <h1>📄 مستند تصميم اللعبة (GDD)</h1>
        <div class="sub" contenteditable="true" id="gameTitle">[اكتب هنا: اسم لعبتك أو شعارها]</div>
        <div class="meta-grid" id="metaGrid">
            <div class="meta-item" contenteditable="true">🎮 النوع: [اكتب هنا]</div>
            <div class="meta-item" contenteditable="true">🕒 المدة المتوقعة: [اكتب هنا]</div>
            <div class="meta-item" contenteditable="true">🖥️ المنصة: [اكتب هنا]</div>
            <div class="meta-item" contenteditable="true">📅 تاريخ الإصدار: [اكتب هنا]</div>
            <div class="meta-item" contenteditable="true">👤 المصمم(ون): [اكتب هنا]</div>
        </div>
    </div>

    <!-- شريط الإعدادات -->
    <div class="setting-bar">
        <div>
            <button class="setting-btn theme-toggle" id="themeToggle">🌙 الوضع المظلم</button>
            <button class="setting-btn" id="saveAllBtn">💾 حفظ كل شيء</button>
            <button class="setting-btn" id="resetBtn">🔄 إعادة تعيين</button>
        </div>
        <div class="save-status" id="saveStatus">✅ تم الحفظ تلقائيًا</div>
    </div>

    <div class="nav-tabs">
        <button class="tab-btn active" data-tab="tab1">🎯 الرؤية</button>
        <button class="tab-btn" data-tab="tab2">🏛️ الركائز</button>
        <button class="tab-btn" data-tab="tab3">🕹️ الميكانيكيات</button>
        <button class="tab-btn" data-tab="tab4">🗺️ المستويات</button>
        <button class="tab-btn" data-tab="tab5">👥 الشخصيات</button>
        <button class="tab-btn" data-tab="tab6">👹 البوسات</button>
        <button class="tab-btn" data-tab="tab7">🎼 الصوت والفن</button>
        <button class="tab-btn" data-tab="tab8">📊 السوق</button>
        <button class="tab-btn" data-tab="tab9">📋 Kanban</button>
        <button class="tab-btn" data-tab="tab10">💻 التقنيات</button>
    </div>

    <div class="content-pane" id="contentPane">
        <!-- قسم 1: الرؤية -->
        <div id="tab1" class="tab-content active-tab">
            <h2>🎯 رؤية اللعبة</h2>
            <div class="editable-field" contenteditable="true" id="visionElevator">
                <strong>مفهوم اللعبة (Elevator Pitch):</strong><br>
                [صف فكرتك الأساسية في 2-3 جمل مختصرة]
            </div>
            <div class="pillar-box" contenteditable="true" id="visionExperience">
                📌 <strong>التجربة الأساسية:</strong><br>
                [ماذا يشعر اللاعب أثناء اللعب؟ ما المشاعر التي تريد إيصالها؟]
            </div>
            <h3>الجمهور المستهدف</h3>
            <div contenteditable="true" id="visionAudience">
                <ul>
                    <li>الفئة العمرية: [اكتب هنا]</li>
                    <li>الألعاب المشابهة التي يحبها: [اكتب هنا]</li>
                    <li>عادات اللعب: [اكتب هنا]</li>
                </ul>
            </div>
        </div>

        <!-- قسم 2: الركائز -->
        <div id="tab2" class="tab-content">
            <h2>🏛️ ركائز التصميم</h2>
            <div id="pillarsContainer">
                <p><strong>القاعدة:</strong> كل قرار تصميمي يجب أن يدعم واحدة أو أكثر من هذه الركائز.</p>
                <table id="pillarsTable">
                    <thead>
                        <tr><th>الركيزة</th><th>الوصف</th><th>مثال تطبيقي</th><th style="width:50px"></th></tr>
                    </thead>
                    <tbody>
                        <tr><td contenteditable="true">[الركيزة 1]</td><td contenteditable="true">[وصفها]</td><td contenteditable="true">[مثال]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                        <tr><td contenteditable="true">[الركيزة 2]</td><td contenteditable="true">[وصفها]</td><td contenteditable="true">[مثال]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                        <tr><td contenteditable="true">[الركيزة 3]</td><td contenteditable="true">[وصفها]</td><td contenteditable="true">[مثال]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                    </tbody>
                </table>
                <button class="add-row-btn" data-table="pillarsTable">+ إضافة ركيزة جديدة</button>
            </div>
        </div>

        <!-- قسم 3: الميكانيكيات -->
        <div id="tab3" class="tab-content">
            <h2>🕹️ الميكانيكيات الأساسية</h2>
            <div contenteditable="true" id="mechanics">
                <h3>[اسم الميكانيكية 1]</h3>
                <ul>
                    <li>الزر/الإدخال: [اكتب هنا]</li>
                    <li>السلوك: [اكتب هنا]</li>
                    <li>التأثير على اللاعب: [اكتب هنا]</li>
                </ul>
                <h3>[اسم الميكانيكية 2]</h3>
                <ul>
                    <li>الزر/الإدخال: [اكتب هنا]</li>
                    <li>السلوك: [اكتب هنا]</li>
                    <li>التأثير على اللاعب: [اكتب هنا]</li>
                </ul>
            </div>
        </div>

        <!-- قسم 4: المستويات -->
        <div id="tab4" class="tab-content">
            <h2>🗺️ هيكل المستويات</h2>
            <div id="levelsContainer">
                <p><strong>التسلسل العام:</strong> [اكتب ترتيب المستويات هنا]</p>
                <table id="levelsTable">
                    <thead><tr><th>المستوى/المنطقة</th><th>الغرض التعليمي</th><th>المدة التقريبية</th><th>العناصر الخاصة</th><th style="width:50px"></th></tr></thead>
                    <tbody>
                        <tr><td contenteditable="true">[المستوى 1]</td><td contenteditable="true">[ماذا يعلم اللاعب؟]</td><td contenteditable="true">[دقائق]</td><td contenteditable="true">[أعداء/ألغاز]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                        <tr><td contenteditable="true">[المستوى 2]</td><td contenteditable="true">[ماذا يعلم اللاعب؟]</td><td contenteditable="true">[دقائق]</td><td contenteditable="true">[أعداء/ألغاز]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                        <tr><td contenteditable="true">[المستوى 3]</td><td contenteditable="true">[ماذا يعلم اللاعب؟]</td><td contenteditable="true">[دقائق]</td><td contenteditable="true">[أعداء/ألغاز]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                    </tbody>
                </table>
                <button class="add-row-btn" data-table="levelsTable">+ إضافة مستوى جديد</button>
            </div>
        </div>

        <!-- قسم 5: الشخصيات (جديد) -->
        <div id="tab5" class="tab-content">
            <h2>👥 الشخصيات</h2>
            <div id="charactersContainer">
                <table id="charactersTable">
                    <thead><tr><th>اسم الشخصية</th><th>الدور في القصة</th><th>القدرات/السمات</th><th>ملاحظات</th><th style="width:50px"></th></tr></thead>
                    <tbody>
                        <tr><td contenteditable="true">[البطل]</td><td contenteditable="true">[الدور]</td><td contenteditable="true">[القدرات]</td><td contenteditable="true">[ملاحظات]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                        <tr><td contenteditable="true">[العدو الرئيسي]</td><td contenteditable="true">[الدور]</td><td contenteditable="true">[القدرات]</td><td contenteditable="true">[ملاحظات]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                    </tbody>
                </table>
                <button class="add-row-btn" data-table="charactersTable">+ إضافة شخصية جديدة</button>
            </div>
        </div>

        <!-- قسم 6: البوسات (جديد) -->
        <div id="tab6" class="tab-content">
            <h2>👹 نظام البوسات والتحديات</h2>
            <div id="bossesContainer">
                <table id="bossesTable">
                    <thead><tr><th>اسم البوس</th><th>الموقع</th><th>طريقة الهزيمة</th><th>المكافأة</th><th style="width:50px"></th></tr></thead>
                    <tbody>
                        <tr><td contenteditable="true">[بوس 1]</td><td contenteditable="true">[أين يظهر؟]</td><td contenteditable="true">[كيف يهزم؟]</td><td contenteditable="true">[المكافأة]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                        <tr><td contenteditable="true">[بوس 2]</td><td contenteditable="true">[أين يظهر؟]</td><td contenteditable="true">[كيف يهزم؟]</td><td contenteditable="true">[المكافأة]</td><td><button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button></td></tr>
                    </tbody>
                </table>
                <button class="add-row-btn" data-table="bossesTable">+ إضافة بوس جديد</button>
            </div>
        </div>

        <!-- قسم 7: الصوت والفن -->
        <div id="tab7" class="tab-content">
            <h2>🎨 الأسلوب البصري والصوتي</h2>
            <div contenteditable="true" id="artAudio">
                <table>
                    <tr><th>العنصر</th><th>التفاصيل</th></tr>
                    <tr><td>الدقة / النمط البصري</td><td>[اكتب هنا، مثل: Pixel Art 16x16]</td></tr>
                    <tr><td>لوحة الألوان</td><td>[اكتب الألوان الرئيسية]</td></tr>
                    <tr><td>الإضاءة</td><td>[نوع الإضاءة وتأثيرها]</td></tr>
                    <tr><td>موسيقى الخلفية</td><td>[الوصف والأجواء]</td></tr>
                    <tr><td>المؤثرات الصوتية الرئيسية</td><td>[أمثلة]</td></tr>
                </table>
            </div>
        </div>

        <!-- قسم 8: السوق -->
        <div id="tab8" class="tab-content">
            <h2>📊 تحليل السوق والجمهور</h2>
            <div contenteditable="true" id="market">
                <p><strong>الفجوة التي تستهدفها اللعبة:</strong> [اكتب هنا]</p>
                <p><strong>الألعاب المنافسة/المشابهة:</strong> [اكتب هنا]</p>
                <p><strong>قنوات التسويق المقترحة:</strong> [اكتب هنا]</p>
                <div class="pillar-box">
                    📢 <strong>خطة النشر:</strong> [متى وأين ستنشر اللعبة؟]
                </div>
            </div>
        </div>

        <!-- قسم 9: Kanban (جديد) -->
        <div id="tab9" class="tab-content">
            <h2>📋 لوحة Kanban - إدارة المهام</h2>
            <div class="kanban-container" id="kanbanContainer">
                <div class="kanban-column" data-status="todo">
                    <div class="kanban-header">
                        <span>📝 قيد الانتظار (To Do)</span>
                        <span class="card-count">0</span>
                    </div>
                    <div class="kanban-cards" id="todoCards"></div>
                    <button class="add-card-btn" data-status="todo">+ إضافة مهمة</button>
                </div>
                <div class="kanban-column" data-status="progress">
                    <div class="kanban-header">
                        <span>⚡ قيد التنفيذ (In Progress)</span>
                        <span class="card-count">0</span>
                    </div>
                    <div class="kanban-cards" id="progressCards"></div>
                    <button class="add-card-btn" data-status="progress">+ إضافة مهمة</button>
                </div>
                <div class="kanban-column" data-status="done">
                    <div class="kanban-header">
                        <span>✅ مكتمل (Done)</span>
                        <span class="card-count">0</span>
                    </div>
                    <div class="kanban-cards" id="doneCards"></div>
                    <button class="add-card-btn" data-status="done">+ إضافة مهمة</button>
                </div>
            </div>
        </div>

        <!-- قسم 10: التقنيات -->
        <div id="tab10" class="tab-content">
            <h2>💻 التقنيات والأدوات</h2>
            <div contenteditable="true" id="tech">
                <table>
                    <tr><th>الغرض</th><th>الأداة المختارة</th><th>السبب</th></tr>
                    <tr><td>محرك اللعبة</td><td>[Godot / Unity / Unreal...]</td><td>[لماذا؟]</td></tr>
                    <tr><td>التحكم بالإصدارات</td><td>[Git / GitHub...]</td><td>[لماذا؟]</td></tr>
                    <tr><td>إدارة المهام</td><td>[Trello / Notion...]</td><td>[لماذا؟]</td></tr>
                    <tr><td>الرسومات</td><td>[Aseprite / Photoshop...]</td><td>[لماذا؟]</td></tr>
                    <tr><td>الصوت والموسيقى</td><td>[Audacity / Pixabay...]</td><td>[لماذا؟]</td></tr>
                </table>
                <div class="code-block" contenteditable="true" id="codeSnippet">
                    // يمكنك إضافة أكواد برمجية نموذجية هنا
                    [اكتب كودك التجريبي أو ملاحظات تقنية]
                </div>
            </div>
        </div>
    </div>

    <div style="padding: 0 35px 20px;">
        <button class="action-print" id="printPDFBtn">🖨️ طباعة / حفظ كـ PDF</button>
    </div>
    <div class="footer-note">
        قالب GDD متكامل مع Kanban وحفظ تلقائي – يمكنك التعديل على جميع الحقول مباشرة.<br>
        تم التطوير وفق منهجية الصفحة الواحدة + Elemental Tetrad
    </div>
</div>

<!-- Modal لإضافة بطاقات Kanban -->
<div id="cardModal" class="modal">
    <div class="modal-content">
        <h3>➕ إضافة مهمة جديدة</h3>
        <input type="text" id="cardTitle" placeholder="عنوان المهمة" style="width:100%">
        <textarea id="cardDesc" placeholder="وصف المهمة (اختياري)" rows="3" style="width:100%"></textarea>
        <button id="saveCardBtn" style="background:#e94560;color:white;border:none;padding:8px 20px;border-radius:25px;cursor:pointer;">إضافة</button>
        <button id="closeModalBtn" style="background:#aaa;color:white;border:none;padding:8px 20px;border-radius:25px;cursor:pointer;">إلغاء</button>
    </div>
</div>

<script>
    // ==================== نظام الحفظ والتحميل ====================
    let currentCardStatus = null;
    let currentEditingCard = null;

    function saveAllToLocalStorage() {
        const data = {
            gameTitle: document.getElementById('gameTitle')?.innerHTML || '',
            metaItems: Array.from(document.querySelectorAll('#metaGrid .meta-item')).map(el => el.innerHTML),
            visionElevator: document.getElementById('visionElevator')?.innerHTML || '',
            visionExperience: document.getElementById('visionExperience')?.innerHTML || '',
            visionAudience: document.getElementById('visionAudience')?.innerHTML || '',
            pillarsTable: document.getElementById('pillarsTable')?.outerHTML || '',
            mechanics: document.getElementById('mechanics')?.innerHTML || '',
            levelsTable: document.getElementById('levelsTable')?.outerHTML || '',
            charactersTable: document.getElementById('charactersTable')?.outerHTML || '',
            bossesTable: document.getElementById('bossesTable')?.outerHTML || '',
            artAudio: document.getElementById('artAudio')?.innerHTML || '',
            market: document.getElementById('market')?.innerHTML || '',
            tech: document.getElementById('tech')?.innerHTML || '',
            codeSnippet: document.getElementById('codeSnippet')?.innerHTML || '',
            kanbanCards: getKanbanCardsData(),
            theme: document.body.className
        };
        localStorage.setItem('gddData', JSON.stringify(data));
        const statusDiv = document.getElementById('saveStatus');
        if (statusDiv) {
            statusDiv.innerHTML = '✅ تم الحفظ تلقائيًا';
            setTimeout(() => { if(statusDiv) statusDiv.innerHTML = '💾 تم الحفظ'; }, 2000);
        }
    }

    function getKanbanCardsData() {
        const cards = { todo: [], progress: [], done: [] };
        document.querySelectorAll('#todoCards .kanban-card').forEach(card => {
            cards.todo.push({ title: card.querySelector('.card-title')?.innerText || '', desc: card.querySelector('.card-desc')?.innerHTML || '' });
        });
        document.querySelectorAll('#progressCards .kanban-card').forEach(card => {
            cards.progress.push({ title: card.querySelector('.card-title')?.innerText || '', desc: card.querySelector('.card-desc')?.innerHTML || '' });
        });
        document.querySelectorAll('#doneCards .kanban-card').forEach(card => {
            cards.done.push({ title: card.querySelector('.card-title')?.innerText || '', desc: card.querySelector('.card-desc')?.innerHTML || '' });
        });
        return cards;
    }

    function loadKanbanCards(data) {
        if (!data) return;
        renderKanbanCards('todo', data.todo || []);
        renderKanbanCards('progress', data.progress || []);
        renderKanbanCards('done', data.done || []);
    }

    function renderKanbanCards(status, cards) {
        const container = status === 'todo' ? document.getElementById('todoCards') :
                         (status === 'progress' ? document.getElementById('progressCards') : document.getElementById('doneCards'));
        if (!container) return;
        container.innerHTML = '';
        cards.forEach(card => {
            addKanbanCardToDOM(status, card.title, card.desc);
        });
        updateCardCounts();
    }

    function addKanbanCardToDOM(status, title, desc) {
        const container = status === 'todo' ? document.getElementById('todoCards') :
                         (status === 'progress' ? document.getElementById('progressCards') : document.getElementById('doneCards'));
        if (!container) return;
        const card = document.createElement('div');
        card.className = 'kanban-card';
        card.draggable = true;
        card.setAttribute('data-status', status);
        card.innerHTML = `
            <span class="card-delete" onclick="deleteCard(this)">🗑️</span>
            <div class="card-title" contenteditable="true">${escapeHtml(title)}</div>
            <div class="card-desc" contenteditable="true">${escapeHtml(desc)}</div>
        `;
        card.addEventListener('dragstart', handleDragStart);
        card.addEventListener('dragend', handleDragEnd);
        container.appendChild(card);
    }

    function escapeHtml(text) { return text.replace(/[&<>]/g, function(m){if(m==='&') return '&amp;'; if(m==='<') return '&lt;'; if(m==='>') return '&gt;'; return m;}); }

    let draggedCard = null;
    function handleDragStart(e) { draggedCard = this; e.dataTransfer.setData('text/plain', ''); }
    function handleDragEnd(e) { draggedCard = null; }

    function updateCardCounts() {
        document.querySelectorAll('.kanban-column').forEach(col => {
            const count = col.querySelectorAll('.kanban-card').length;
            const countSpan = col.querySelector('.card-count');
            if (countSpan) countSpan.innerText = count;
        });
    }

    function deleteCard(btn) { btn.closest('.kanban-card')?.remove(); updateCardCounts(); saveAllToLocalStorage(); }

    function loadAllFromLocalStorage() {
        const saved = localStorage.getItem('gddData');
        if (!saved) return;
        try {
            const data = JSON.parse(saved);
            if (data.gameTitle) document.getElementById('gameTitle').innerHTML = data.gameTitle;
            if (data.metaItems) {
                const metaItems = document.querySelectorAll('#metaGrid .meta-item');
                data.metaItems.forEach((html, idx) => { if(metaItems[idx]) metaItems[idx].innerHTML = html; });
            }
            if (data.visionElevator) document.getElementById('visionElevator').innerHTML = data.visionElevator;
            if (data.visionExperience) document.getElementById('visionExperience').innerHTML = data.visionExperience;
            if (data.visionAudience) document.getElementById('visionAudience').innerHTML = data.visionAudience;
            if (data.pillarsTable) document.getElementById('pillarsTable').outerHTML = data.pillarsTable;
            if (data.mechanics) document.getElementById('mechanics').innerHTML = data.mechanics;
            if (data.levelsTable) document.getElementById('levelsTable').outerHTML = data.levelsTable;
            if (data.charactersTable) document.getElementById('charactersTable').outerHTML = data.charactersTable;
            if (data.bossesTable) document.getElementById('bossesTable').outerHTML = data.bossesTable;
            if (data.artAudio) document.getElementById('artAudio').innerHTML = data.artAudio;
            if (data.market) document.getElementById('market').innerHTML = data.market;
            if (data.tech) document.getElementById('tech').innerHTML = data.tech;
            if (data.codeSnippet) document.getElementById('codeSnippet').innerHTML = data.codeSnippet;
            if (data.kanbanCards) loadKanbanCards(data.kanbanCards);
            if (data.theme) document.body.className = data.theme;
            attachDeleteButtons();
            attachDragDrop();
        } catch(e) { console.error('خطأ في التحميل', e); }
    }

    function attachDeleteButtons() {
        document.querySelectorAll('.delete-row-btn').forEach(btn => {
            btn.onclick = function() { this.closest('tr')?.remove(); saveAllToLocalStorage(); };
        });
    }

    function attachDragDrop() {
        document.querySelectorAll('.kanban-cards').forEach(container => {
            container.addEventListener('dragover', e => e.preventDefault());
            container.addEventListener('drop', e => {
                e.preventDefault();
                if (draggedCard) {
                    const newStatus = container.closest('.kanban-column')?.getAttribute('data-status');
                    if (newStatus) {
                        draggedCard.setAttribute('data-status', newStatus);
                        container.appendChild(draggedCard);
                        updateCardCounts();
                        saveAllToLocalStorage();
                    }
                }
            });
        });
    }

    // إضافة صفوف للجداول
    function addTableRow(tableId) {
        const table = document.getElementById(tableId);
        const tbody = table.querySelector('tbody');
        const newRow = tbody.insertRow();
        const colCount = table.rows[0]?.cells.length - 1 || 3;
        for(let i = 0; i < colCount; i++) {
            const cell = newRow.insertCell(i);
            cell.setAttribute('contenteditable', 'true');
            cell.innerText = '[جديد]';
        }
        const deleteCell = newRow.insertCell(colCount);
        deleteCell.innerHTML = '<button class="delete-row-btn" style="background:#e94560;border:none;color:white;border-radius:50%;width:25px;cursor:pointer;">✖</button>';
        deleteCell.querySelector('.delete-row-btn').onclick = function() { this.closest('tr')?.remove(); saveAllToLocalStorage(); };
        saveAllToLocalStorage();
    }

    // إضافة بطاقة Kanban
    function showAddCardModal(status) {
        currentCardStatus = status;
        document.getElementById('cardModal').style.display = 'flex';
    }

    function addKanbanCard() {
        const title = document.getElementById('cardTitle').value.trim();
        const desc = document.getElementById('cardDesc').value.trim();
        if (!title) return;
        addKanbanCardToDOM(currentCardStatus, title, desc);
        updateCardCounts();
        document.getElementById('cardModal').style.display = 'none';
        document.getElementById('cardTitle').value = '';
        document.getElementById('cardDesc').value = '';
        saveAllToLocalStorage();
    }

    // التبديل بين التبويبات
    const tabs = document.querySelectorAll('.tab-btn');
    const contents = document.querySelectorAll('.tab-content');
    tabs.forEach(btn => {
        btn.addEventListener('click', () => {
            const tabId = btn.getAttribute('data-tab');
            contents.forEach(content => content.classList.remove('active-tab'));
            document.getElementById(tabId).classList.add('active-tab');
            tabs.forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
        });
    });

    // الوضع المظلم
    document.getElementById('themeToggle')?.addEventListener('click', () => {
        const isDark = document.body.classList.contains('dark-mode');
        if (isDark) {
            document.body.classList.remove('dark-mode');
            document.body.classList.add('light-mode');
            document.getElementById('themeToggle').innerHTML = '🌙 الوضع المظلم';
        } else {
            document.body.classList.remove('light-mode');
            document.body.classList.add('dark-mode');
            document.getElementById('themeToggle').innerHTML = '☀️ الوضع الفاتح';
        }
        saveAllToLocalStorage();
    });

    // الطباعة
    document.getElementById('printPDFBtn')?.addEventListener('click', () => window.print());

    // حفظ يدوي
    document.getElementById('saveAllBtn')?.addEventListener('click', () => { saveAllToLocalStorage(); alert('تم حفظ كل شيء!'); });

    // إعادة تعيين
    document.getElementById('resetBtn')?.addEventListener('click', () => {
        if(confirm('هل أنت متأكد؟ سيتم حذف كل البيانات المدخلة!')) {
            localStorage.removeItem('gddData');
            location.reload();
        }
    });

    // إضافة صفوف للجداول
    document.querySelectorAll('.add-row-btn').forEach(btn => {
        const tableId = btn.getAttribute('data-table');
        if(tableId) btn.onclick = () => addTableRow(tableId);
    });

    // Kanban
    document.querySelectorAll('.add-card-btn').forEach(btn => {
        const status = btn.getAttribute('data-status');
        btn.onclick = () => showAddCardModal(status);
    });
    document.getElementById('saveCardBtn')?.addEventListener('click', addKanbanCard);
    document.getElementById('closeModalBtn')?.addEventListener('click', () => document.getElementById('cardModal').style.display = 'none');
    window.onclick = (e) => { if(e.target === document.getElementById('cardModal')) document.getElementById('cardModal').style.display = 'none'; };

    window.deleteCard = deleteCard;
    window.addTableRow = addTableRow;

    // حفظ تلقائي عند التعديل
    document.querySelectorAll('[contenteditable="true"]').forEach(el => {
        el.addEventListener('input', () => saveAllToLocalStorage());
    });

    // تحميل البيانات عند بدء التشغيل
    loadAllFromLocalStorage();
    attachDragDrop();
    updateCardCounts();
</script>
</body>
</html>
