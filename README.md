<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.5, user-scalable=yes">
    <title>国际计算器 · 带公式导出</title>
    <style>
        :root {
            --bg: #f4f7fb;
            --card-bg: #ffffff;
            --primary: #1e3a5f;
            --primary-light: #2c5282;
            --accent: #e07b39;
            --accent-hover: #c96a2e;
            --green: #2f855a;
            --green-light: #e6fffa;
            --orange: #dd6b20;
            --orange-light: #fffaf0;
            --purple: #6b46c1;
            --purple-light: #faf5ff;
            --blue: #3182ce;
            --blue-light: #ebf8ff;
            --text: #1e2b3a;
            --text-light: #5e6f82;
            --border: #dce3ec;
            --shadow: 0 10px 30px rgba(0, 20, 40, 0.08);
            --radius: 20px;
            --radius-sm: 12px;
            --transition: 0.2s ease;
            --font: 'Inter', 'Segoe UI', 'PingFang SC', 'Microsoft YaHei', sans-serif;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background: linear-gradient(145deg, #f0f4fa 0%, #e8edf5 100%);
            font-family: var(--font);
            color: var(--text);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 1.5rem 1rem;
        }

        .app-container {
            max-width: 950px;
            width: 100%;
            background: var(--card-bg);
            border-radius: var(--radius);
            box-shadow: var(--shadow);
            padding: 2rem 2rem 2.5rem;
            border: 1px solid rgba(255, 255, 255, 0.6);
        }

        h1 {
            font-size: 1.8rem;
            font-weight: 600;
            letter-spacing: -0.02em;
            color: var(--primary);
            display: flex;
            align-items: center;
            gap: 0.6rem;
            margin-bottom: 1.2rem;
            border-bottom: 2px solid var(--border);
            padding-bottom: 1rem;
        }

        h1 .icon {
            font-size: 2rem;
        }

        .section-title {
            font-weight: 600;
            font-size: 1rem;
            color: var(--primary-light);
            margin-bottom: 0.8rem;
            display: flex;
            align-items: center;
            gap: 0.4rem;
            flex-wrap: wrap;
        }

        .section-badge {
            background: #eef3f9;
            padding: 0.2rem 0.7rem;
            border-radius: 30px;
            font-size: 0.7rem;
            font-weight: 600;
            color: var(--primary-light);
            letter-spacing: 0.03em;
        }

        .tag-green { background: var(--green-light); color: var(--green); padding: 0.15rem 0.7rem; border-radius: 30px; font-size: 0.7rem; font-weight: 600; }
        .tag-orange { background: var(--orange-light); color: var(--orange); padding: 0.15rem 0.7rem; border-radius: 30px; font-size: 0.7rem; font-weight: 600; }
        .tag-purple { background: var(--purple-light); color: var(--purple); padding: 0.15rem 0.7rem; border-radius: 30px; font-size: 0.7rem; font-weight: 600; }
        .tag-blue { background: var(--blue-light); color: var(--blue); padding: 0.15rem 0.7rem; border-radius: 30px; font-size: 0.7rem; font-weight: 600; }

        .input-group {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 1.2rem;
        }

        .input-field {
            flex: 1 1 150px;
            display: flex;
            flex-direction: column;
            gap: 0.4rem;
        }

        .input-field label {
            font-weight: 500;
            font-size: 0.85rem;
            color: var(--text-light);
            letter-spacing: 0.02em;
        }

        .input-field input {
            border: 1.5px solid var(--border);
            border-radius: var(--radius-sm);
            padding: 0.8rem 1rem;
            font-size: 1rem;
            font-weight: 500;
            background: #fafcff;
            transition: border 0.15s, box-shadow 0.15s;
            outline: none;
            width: 100%;
        }

        .input-field input:focus {
            border-color: var(--primary-light);
            box-shadow: 0 0 0 4px rgba(44, 82, 130, 0.1);
            background: white;
        }

        .input-field input[type="number"] { -moz-appearance: textfield; }
        .input-field input[type="number"]::-webkit-outer-spin-button,
        .input-field input[type="number"]::-webkit-inner-spin-button { -webkit-appearance: none; margin: 0; }

        .btn-primary {
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 40px;
            padding: 1rem 2rem;
            font-size: 1.15rem;
            font-weight: 600;
            letter-spacing: 0.02em;
            cursor: pointer;
            transition: background var(--transition), transform 0.1s ease;
            box-shadow: 0 8px 20px rgba(30, 58, 95, 0.25);
            width: 100%;
            margin-top: 0.8rem;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }
        .btn-primary:hover { background: var(--primary-light); box-shadow: 0 12px 28px rgba(30, 58, 95, 0.35); }
        .btn-primary:active { transform: scale(0.98); background: #162b42; }

        .btn-export {
            background: var(--green);
            color: white;
            border: none;
            border-radius: 40px;
            padding: 0.9rem 1.5rem;
            font-size: 1rem;
            font-weight: 600;
            letter-spacing: 0.02em;
            cursor: pointer;
            transition: background var(--transition), transform 0.1s ease;
            box-shadow: 0 6px 16px rgba(47, 133, 90, 0.25);
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
        }
        .btn-export:hover { background: #276749; box-shadow: 0 8px 20px rgba(47, 133, 90, 0.35); }
        .btn-export:active { transform: scale(0.98); }

        .btn-group {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }
        .btn-group .btn-primary, .btn-group .btn-export { flex: 1; min-width: 150px; }

        .divider { height: 1px; background: linear-gradient(to right, var(--border), transparent); margin: 1.8rem 0 1.5rem; }

        /* 谷子类型卡片 */
        .grain-types-container {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 1.2rem;
        }

        .grain-type-card {
            background: #fafbff;
            border: 1.5px solid var(--border);
            border-radius: var(--radius-sm);
            padding: 1rem 1.2rem;
            display: flex;
            align-items: center;
            gap: 0.8rem;
            flex-wrap: wrap;
            flex: 1 1 220px;
            transition: all 0.15s;
        }
        .grain-type-card:hover { border-color: #b6c8dd; }

        .grain-type-card .type-name-input {
            flex: 1;
            min-width: 80px;
            border: none;
            border-bottom: 2px dashed #cbd5e1;
            background: transparent;
            padding: 0.3rem 0.2rem;
            font-size: 0.95rem;
            font-weight: 600;
            color: var(--primary);
            outline: none;
            transition: border 0.15s;
        }
        .grain-type-card .type-name-input:focus { border-bottom-color: var(--primary-light); }

        .grain-type-card .weight-input {
            width: 70px;
            border: 1px solid var(--border);
            border-radius: 6px;
            padding: 0.35rem 0.3rem;
            font-size: 0.85rem;
            text-align: center;
            background: white;
            outline: none;
        }
        .grain-type-card .weight-input:focus { border-color: var(--purple); box-shadow: 0 0 0 3px rgba(107, 70, 193, 0.1); }
        .grain-type-card .unit { font-size: 0.8rem; color: var(--text-light); }

        .remove-type-btn {
            background: none;
            border: none;
            color: #b0c0d0;
            cursor: pointer;
            font-size: 1.2rem;
            line-height: 1;
            padding: 0 0.3rem;
            transition: color 0.2s;
        }
        .remove-type-btn:hover { color: #d43f3f; }

        .add-type-btn {
            background: transparent;
            border: 2px dashed #b7c6da;
            color: var(--primary-light);
            border-radius: 40px;
            padding: 0.6rem 1.2rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            font-size: 0.9rem;
        }
        .add-type-btn:hover { border-color: var(--primary-light); background: #f0f5fc; }

        /* 包装总克重卡片 */
        .packaging-total-card {
            background: #fffbf5;
            border: 1.5px solid #f0e0cc;
            border-radius: var(--radius-sm);
            padding: 1rem 1.2rem;
            display: flex;
            align-items: center;
            gap: 0.8rem;
            flex-wrap: wrap;
            max-width: 300px;
            margin-bottom: 1.2rem;
        }
        .packaging-total-card .label {
            font-weight: 600;
            color: var(--orange);
        }
        .packaging-total-card input {
            width: 100px;
            border: 1px solid #e8d5c0;
            border-radius: 6px;
            padding: 0.35rem 0.3rem;
            font-size: 0.85rem;
            text-align: center;
            background: white;
            outline: none;
        }
        .packaging-total-card input:focus { border-color: var(--orange); box-shadow: 0 0 0 3px rgba(221, 107, 32, 0.1); }
        .packaging-total-card .unit { font-size: 0.8rem; color: var(--text-light); }

        /* 表格 */
        .table-wrapper {
            overflow-x: auto;
            margin: 1rem 0;
            border-radius: var(--radius-sm);
            border: 1px solid var(--border);
            background: white;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 700px;
            font-size: 0.88rem;
        }

        th {
            background: #f0f4fa;
            color: var(--primary);
            font-weight: 600;
            padding: 0.8rem 0.5rem;
            text-align: left;
            border-bottom: 2px solid #cbd6e4;
            white-space: nowrap;
        }

        td {
            padding: 0.7rem 0.5rem;
            border-bottom: 1px solid #e2e8f0;
            vertical-align: middle;
        }

        tr:last-child td { border-bottom: none; }

        .name-input-cell input {
            width: 90px;
            border: none;
            border-bottom: 2px dashed #cbd5e1;
            background: transparent;
            padding: 0.25rem 0.2rem;
            font-size: 0.9rem;
            font-weight: 500;
            outline: none;
        }
        .name-input-cell input:focus { border-bottom-color: var(--primary-light); }

        .member-grain-select {
            display: flex;
            flex-wrap: wrap;
            gap: 0.5rem;
            align-items: center;
        }

        .grain-select-item {
            display: flex;
            align-items: center;
            gap: 0.3rem;
            background: #f7fafd;
            padding: 0.2rem 0.5rem;
            border-radius: 6px;
            border: 1px solid #e2e8f0;
        }
        .grain-select-item select {
            border: none;
            background: transparent;
            font-size: 0.8rem;
            padding: 0.2rem;
            outline: none;
        }
        .grain-select-item input[type="number"] {
            width: 45px;
            border: 1px solid #e2e8f0;
            border-radius: 4px;
            padding: 0.2rem;
            text-align: center;
            font-size: 0.8rem;
        }

        .total-grams-cell {
            font-weight: 600;
            color: var(--text-light);
            text-align: right;
            min-width: 70px;
        }

        .amount-cell {
            font-weight: 700;
            color: var(--primary);
            text-align: right;
            min-width: 80px;
        }

        .remove-cell button {
            background: none;
            border: none;
            color: #b0c0d0;
            cursor: pointer;
            font-size: 1.4rem;
            line-height: 1;
            padding: 0 0.4rem;
            transition: color 0.2s;
        }
        .remove-cell button:hover { color: #d43f3f; }

        .add-member-btn {
            background: transparent;
            border: 2px dashed #b7c6da;
            color: var(--primary-light);
            border-radius: 40px;
            padding: 0.7rem 1.5rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: 0.5rem;
            width: 100%;
            margin-top: 0.5rem;
        }
        .add-member-btn:hover { border-color: var(--primary-light); background: #f0f5fc; }

        /* 汇总 */
        .summary-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
            gap: 1rem;
            background: #f5f9ff;
            border-radius: var(--radius-sm);
            padding: 1.5rem 1.8rem;
            border: 1px solid #dbe6f2;
            margin-top: 1rem;
        }
        .summary-item { display: flex; flex-direction: column; gap: 0.25rem; }
        .summary-label { font-size: 0.75rem; font-weight: 600; color: #4d637c; text-transform: uppercase; letter-spacing: 0.04em; }
        .summary-value { font-size: 1.4rem; font-weight: 700; color: var(--primary); line-height: 1.2; }
        .summary-value small { font-size: 0.85rem; font-weight: 500; color: #54738f; }

        .footer-note {
            margin-top: 1.8rem;
            font-size: 0.8rem;
            color: #8b9eb0;
            text-align: center;
            border-top: 1px solid #e4eaf2;
            padding-top: 1.2rem;
        }

        .error-msg {
            color: #c53030;
            background: #fff5f5;
            border-radius: 8px;
            padding: 0.6rem 1rem;
            margin-bottom: 1rem;
            font-size: 0.9rem;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 0.5rem;
            border: 1px solid #fad1d1;
        }
        .hidden { display: none; }

        @media (max-width: 700px) {
            .app-container { padding: 1.2rem 1rem; }
            .summary-grid { padding: 1rem; grid-template-columns: 1fr 1fr; }
            .summary-value { font-size: 1.2rem; }
            th, td { padding: 0.6rem 0.4rem; font-size: 0.8rem; }
        }
    </style>
</head>
<body>
    <div class="app-container">
        <h1>
            <span class="icon">🌍</span> 国际计算器
        </h1>

        <!-- 费用设置 -->
        <div class="section-title">💰 总费用设置 <span class="section-badge">只需国际运费总价</span></div>
        <div class="input-group">
            <div class="input-field">
                <label>国际运费总价</label>
                <input type="number" id="totalShippingAmount" placeholder="0.00" min="0" step="0.01" value="300.00">
            </div>
            <div class="input-field">
                <label>货币符号</label>
                <input type="text" id="currencySymbol" placeholder="€" value="€" maxlength="5" style="font-weight:600;">
            </div>
        </div>

        <!-- 谷子类型库 -->
        <div class="section-title">📋 谷子类型库 <span class="tag-purple">点击名称可修改</span> <span class="tag-blue">同类型只需测一次克重</span></div>
        <div id="grainTypesContainer" class="grain-types-container"></div>
        <button id="addGrainTypeBtn" class="add-type-btn">＋ 添加谷子类型</button>

        <!-- 包装总克重 -->
        <div class="section-title" style="margin-top: 1rem;">📦 包装总克重 <span class="tag-orange">所有包装合计</span></div>
        <div class="packaging-total-card">
            <span class="label">总克重</span>
            <input type="number" id="totalPackagingGrams" min="0" step="0.1" value="245">
            <span class="unit">g</span>
        </div>

        <!-- 成员表格 -->
        <div class="section-title" style="margin-top: 1.5rem;">👥 成员明细 <span class="tag-blue">谷子类型×数量</span> <span class="tag-orange">包装克重平均分配</span></div>
        <div class="table-wrapper">
            <table id="memberTable">
                <thead>
                    <tr>
                        <th style="width:12%;">姓名</th>
                        <th style="width:35%;">所吃谷子</th>
                        <th style="width:12%;">包装克重(g)</th>
                        <th style="width:15%; text-align:right;">总克重</th>
                        <th style="width:18%; text-align:right;">应摊运费</th>
                        <th style="width:8%;"></th>
                    </tr>
                </thead>
                <tbody id="tableBody"></tbody>
            </table>
        </div>
        <button id="addMemberBtn" class="add-member-btn">＋ 添加成员</button>

        <div class="btn-group" style="margin-top: 1rem;">
            <button id="calculateBtn" class="btn-primary">🧮 按克重比例分摊运费</button>
            <button id="exportBtn" class="btn-export">📥 导出Excel（带公式）</button>
        </div>

        <div class="divider"></div>
        <div class="summary-grid">
            <div class="summary-item"><span class="summary-label">谷子总克重</span><span class="summary-value" id="totalGrainGrams">0.0 <small>g</small></span></div>
            <div class="summary-item"><span class="summary-label">包装总克重</span><span class="summary-value" id="totalPackGramsDisplay">0.0 <small>g</small></span></div>
            <div class="summary-item"><span class="summary-label">总克重合计</span><span class="summary-value" id="totalCombinedGrams">0.0 <small>g</small></span></div>
            <div class="summary-item"><span class="summary-label">运费总额</span><span class="summary-value" id="displayShippingAmount">0.00 <small id="shipCur"></small></span></div>
            <div class="summary-item"><span class="summary-label">每克单价</span><span class="summary-value" id="perGramPrice">0.000 <small id="perGramCur"></small></span></div>
        </div>

        <div class="footer-note">
            💡 每位成员应摊运费 = (个人谷子总克重 + 个人包装克重) ÷ 全体成员总克重 × 国际运费总价。<br>
            包装总克重会在所有成员之间平均分配（即每人分得 包装总克重 ÷ 成员数）。<br>
            📥 导出的Excel文件包含完整计算公式，可在Excel中修改数据后自动重算。
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js">
    </script>
    <script>
        (function() {
            // ---------- 初始谷子类型 ----------
            let grainTypes = [
                { id: 'gt1', name: '普通谷子', weightPerUnit: 50 },
                { id: 'gt2', name: '大颗粒谷子', weightPerUnit: 80 },
                { id: 'gt3', name: '混合坚果', weightPerUnit: 120 }
            ];

            // ---------- 初始成员 ----------
            let members = [
                { 
                    id: 'm1', 
                    name: 'Alice', 
                    grainItems: [
                        { typeId: 'gt1', quantity: 3 },
                        { typeId: 'gt2', quantity: 1 }
                    ]
                },
                { 
                    id: 'm2', 
                    name: 'Bob', 
                    grainItems: [
                        { typeId: 'gt2', quantity: 2 },
                        { typeId: 'gt3', quantity: 1 }
                    ]
                },
                { 
                    id: 'm3', 
                    name: 'Charlie', 
                    grainItems: [
                        { typeId: 'gt1', quantity: 5 },
                        { typeId: 'gt3', quantity: 2 }
                    ]
                }
            ];

            let nextGrainTypeId = 4;
            let nextMemberId = 4;

            // DOM元素
            const grainTypesContainer = document.getElementById('grainTypesContainer');
            const tableBody = document.getElementById('tableBody');
            const addGrainTypeBtn = document.getElementById('addGrainTypeBtn');
            const addMemberBtn = document.getElementById('addMemberBtn');
            const calculateBtn = document.getElementById('calculateBtn');
            const exportBtn = document.getElementById('exportBtn');
            const totalShippingInput = document.getElementById('totalShippingAmount');
            const totalPackagingGramsInput = document.getElementById('totalPackagingGrams');
            const currencySymbolInput = document.getElementById('currencySymbol');
            const errorBox = document.getElementById('errorBox');
            const errorText = document.getElementById('errorText');

            // 汇总元素
            const totalGrainGramsDisplay = document.getElementById('totalGrainGrams');
            const totalPackGramsDisplay = document.getElementById('totalPackGramsDisplay');
            const totalCombinedGramsDisplay = document.getElementById('totalCombinedGrams');
            const displayShippingAmount = document.getElementById('displayShippingAmount');
            const perGramPriceDisplay = document.getElementById('perGramPrice');
            const shipCur = document.getElementById('shipCur');
            const perGramCur = document.getElementById('perGramCur');

            // ---------- 渲染谷子类型 ----------
            function renderGrainTypes() {
                grainTypesContainer.innerHTML = '';
                grainTypes.forEach((type, idx) => {
                    const card = document.createElement('div');
                    card.className = 'grain-type-card';

                    const nameInput = document.createElement('input');
                    nameInput.type = 'text';
                    nameInput.className = 'type-name-input';
                    nameInput.value = type.name;
                    nameInput.placeholder = '输入名称';
                    nameInput.title = '点击修改谷子名称';
                    nameInput.addEventListener('input', (e) => {
                        grainTypes[idx].name = e.target.value;
                        renderMemberTable();
                    });

                    const weightInput = document.createElement('input');
                    weightInput.type = 'number';
                    weightInput.min = '0';
                    weightInput.step = '0.1';
                    weightInput.className = 'weight-input';
                    weightInput.value = type.weightPerUnit;
                    weightInput.title = '单个克重(g)';
                    weightInput.addEventListener('input', (e) => {
                        const val = parseFloat(e.target.value);
                        grainTypes[idx].weightPerUnit = isNaN(val) ? 0 : val;
                    });

                    const unitSpan = document.createElement('span');
                    unitSpan.className = 'unit';
                    unitSpan.textContent = 'g/个';

                    const removeBtn = document.createElement('button');
                    removeBtn.className = 'remove-type-btn';
                    removeBtn.innerHTML = '&times;';
                    removeBtn.title = '删除该类型';
                    removeBtn.addEventListener('click', () => removeGrainType(type.id));

                    card.appendChild(nameInput);
                    card.appendChild(weightInput);
                    card.appendChild(unitSpan);
                    card.appendChild(removeBtn);
                    grainTypesContainer.appendChild(card);
                });
                renderMemberTable();
            }

            function removeGrainType(typeId) {
                if (grainTypes.length <= 1) { showError('至少保留一种谷子类型'); return; }
                grainTypes = grainTypes.filter(t => t.id !== typeId);
                members.forEach(m => { m.grainItems = m.grainItems.filter(item => item.typeId !== typeId); });
                renderGrainTypes();
            }

            // ---------- 渲染成员表格 ----------
            function renderMemberTable() {
                tableBody.innerHTML = '';
                const perMemberPackaging = getPerMemberPackagingGrams();

                members.forEach((member, mIdx) => {
                    const row = document.createElement('tr');

                    const nameCell = document.createElement('td');
                    nameCell.className = 'name-input-cell';
                    const nameInput = document.createElement('input');
                    nameInput.type = 'text';
                    nameInput.placeholder = '姓名';
                    nameInput.value = member.name;
                    nameInput.addEventListener('input', (e) => { members[mIdx].name = e.target.value; });
                    nameCell.appendChild(nameInput);

                    const grainCell = document.createElement('td');
                    const grainSelectDiv = document.createElement('div');
                    grainSelectDiv.className = 'member-grain-select';
                    member.grainItems.forEach((item, gIdx) => {
                        const itemDiv = document.createElement('div');
                        itemDiv.className = 'grain-select-item';
                        const select = document.createElement('select');
                        grainTypes.forEach(type => {
                            const opt = document.createElement('option');
                            opt.value = type.id;
                            opt.textContent = type.name;
                            if (type.id === item.typeId) opt.selected = true;
                            select.appendChild(opt);
                        });
                        select.addEventListener('change', (e) => {
                            members[mIdx].grainItems[gIdx].typeId = e.target.value;
                        });
                        const qtyInput = document.createElement('input');
                        qtyInput.type = 'number';
                        qtyInput.min = '0';
                        qtyInput.step = '0.1';
                        qtyInput.value = item.quantity;
                        qtyInput.title = '数量';
                        qtyInput.addEventListener('input', (e) => {
                            const val = parseFloat(e.target.value);
                            members[mIdx].grainItems[gIdx].quantity = isNaN(val) ? 0 : val;
                        });
                        const removeItemBtn = document.createElement('button');
                        removeItemBtn.className = 'remove-type-btn';
                        removeItemBtn.innerHTML = '×';
                        removeItemBtn.style.fontSize = '1rem';
                        removeItemBtn.title = '移除该谷子项';
                        removeItemBtn.addEventListener('click', () => {
                            members[mIdx].grainItems.splice(gIdx, 1);
                            renderMemberTable();
                        });
                        itemDiv.appendChild(select);
                        itemDiv.appendChild(qtyInput);
                        itemDiv.appendChild(removeItemBtn);
                        grainSelectDiv.appendChild(itemDiv);
                    });
                    const addGrainBtn = document.createElement('button');
                    addGrainBtn.className = 'add-type-btn';
                    addGrainBtn.style.padding = '0.2rem 0.6rem';
                    addGrainBtn.style.fontSize = '0.75rem';
                    addGrainBtn.textContent = '+ 谷子';
                    addGrainBtn.addEventListener('click', () => {
                        if (grainTypes.length === 0) { showError('请先添加谷子类型'); return; }
                        members[mIdx].grainItems.push({ typeId: grainTypes[0].id, quantity: 1 });
                        renderMemberTable();
                    });
                    grainSelectDiv.appendChild(addGrainBtn);
                    grainCell.appendChild(grainSelectDiv);

                    const packCell = document.createElement('td');
                    packCell.style.textAlign = 'center';
                    packCell.style.fontWeight = '600';
                    packCell.style.color = 'var(--orange)';
                    packCell.textContent = perMemberPackaging.toFixed(1);

                    const totalGramsCell = document.createElement('td');
                    totalGramsCell.className = 'total-grams-cell';
                    totalGramsCell.id = `total-grams-${mIdx}`;
                    totalGramsCell.textContent = '0.0';

                    const amountCell = document.createElement('td');
                    amountCell.className = 'amount-cell';
                    amountCell.id = `amount-${mIdx}`;
                    amountCell.textContent = '0.00';

                    const removeCell = document.createElement('td');
                    removeCell.className = 'remove-cell';
                    const removeBtn = document.createElement('button');
                    removeBtn.innerHTML = '&times;';
                    removeBtn.title = '移除该成员';
                    removeBtn.addEventListener('click', () => removeMember(mIdx));
                    removeCell.appendChild(removeBtn);

                    row.appendChild(nameCell);
                    row.appendChild(grainCell);
                    row.appendChild(packCell);
                    row.appendChild(totalGramsCell);
                    row.appendChild(amountCell);
                    row.appendChild(removeCell);
                    tableBody.appendChild(row);
                });

                updateCurrencyBadges();
                updateSummaryDisplay();
            }

            function getPerMemberPackagingGrams() {
                const totalPackaging = parseFloat(totalPackagingGramsInput.value) || 0;
                const memberCount = members.length;
                return memberCount > 0 ? totalPackaging / memberCount : 0;
            }

            function removeMember(index) {
                if (members.length <= 1) { showError('至少保留一位成员'); return; }
                members.splice(index, 1);
                renderMemberTable();
                clearAmounts();
            }

            function clearAmounts() {
                document.querySelectorAll('.amount-cell').forEach(el => {
                    if (el.id.startsWith('amount-')) el.textContent = '0.00';
                });
                document.querySelectorAll('.total-grams-cell').forEach(el => {
                    if (el.id.startsWith('total-grams-')) el.textContent = '0.0';
                });
            }

            function showError(msg) {
                errorBox.classList.remove('hidden');
                errorText.textContent = msg;
                setTimeout(() => errorBox.classList.add('hidden'), 4000);
            }
            function hideError() { errorBox.classList.add('hidden'); }

            // ---------- 计算核心 ----------
            function calculateAndDisplay() {
                hideError();

                const shippingTotal = parseFloat(totalShippingInput.value);
                if (isNaN(shippingTotal) || shippingTotal < 0) { showError('国际运费总价无效'); return; }

                const totalPackagingGrams = parseFloat(totalPackagingGramsInput.value) || 0;
                const perMemberPackaging = getPerMemberPackagingGrams();

                const memberGrainGrams = members.map(m => {
                    let totalGrams = 0;
                    m.grainItems.forEach(item => {
                        const type = grainTypes.find(t => t.id === item.typeId);
                        if (type && !isNaN(type.weightPerUnit) && type.weightPerUnit >= 0) {
                            totalGrams += type.weightPerUnit * (parseFloat(item.quantity) || 0);
                        }
                    });
                    return totalGrams;
                });

                const memberTotalGrams = memberGrainGrams.map(g => g + perMemberPackaging);
                const totalCombinedGrams = memberTotalGrams.reduce((s, v) => s + v, 0);

                if (totalCombinedGrams <= 0) { showError('总克重必须大于0'); return; }

                const perGramPrice = shippingTotal / totalCombinedGrams;

                members.forEach((member, index) => {
                    const totalGramsCell = document.getElementById(`total-grams-${index}`);
                    if (totalGramsCell) totalGramsCell.textContent = memberTotalGrams[index].toFixed(1);

                    const amountCell = document.getElementById(`amount-${index}`);
                    if (amountCell) {
                        const amount = memberTotalGrams[index] * perGramPrice;
                        amountCell.textContent = amount.toFixed(2);
                    }
                });

                const totalGrainGrams = memberGrainGrams.reduce((s, v) => s + v, 0);
                updateSummaryDisplay(totalGrainGrams, totalPackagingGrams, totalCombinedGrams, shippingTotal, perGramPrice);
            }

            function updateSummaryDisplay(forceGrainGrams, forcePackGrams, forceCombinedGrams, forceShipAmt, forcePerGram) {
                const shipAmount = forceShipAmt !== undefined ? forceShipAmt : parseFloat(totalShippingInput.value) || 0;

                let totalGrainGrams = forceGrainGrams;
                if (totalGrainGrams === undefined) {
                    totalGrainGrams = members.reduce((sum, m) => {
                        let grams = 0;
                        m.grainItems.forEach(item => {
                            const type = grainTypes.find(t => t.id === item.typeId);
                            if (type && !isNaN(type.weightPerUnit)) grams += type.weightPerUnit * (parseFloat(item.quantity) || 0);
                        });
                        return sum + grams;
                    }, 0);
                }

                const totalPackGrams = forcePackGrams !== undefined ? forcePackGrams : (parseFloat(totalPackagingGramsInput.value) || 0);
                const combinedGrams = forceCombinedGrams !== undefined ? forceCombinedGrams : totalGrainGrams + totalPackGrams;
                const perGram = forcePerGram !== undefined ? forcePerGram : (combinedGrams > 0 ? shipAmount / combinedGrams : 0);

                if (totalGrainGramsDisplay) totalGrainGramsDisplay.textContent = totalGrainGrams.toFixed(1);
                if (totalPackGramsDisplay) totalPackGramsDisplay.textContent = totalPackGrams.toFixed(1);
                if (totalCombinedGramsDisplay) totalCombinedGramsDisplay.textContent = combinedGrams.toFixed(1);
                if (displayShippingAmount) displayShippingAmount.textContent = shipAmount.toFixed(2);
                if (perGramPriceDisplay) perGramPriceDisplay.textContent = perGram.toFixed(3);

                const symbol = currencySymbolInput.value.trim() || '€';
                if (shipCur) shipCur.textContent = symbol;
                if (perGramCur) perGramCur.textContent = `${symbol}/g`;
            }

            function updateCurrencyBadges() {
                const symbol = currencySymbolInput.value.trim() || '€';
                if (shipCur) shipCur.textContent = symbol;
                if (perGramCur) perGramCur.textContent = `${symbol}/g`;
            }

            // ---------- 添加谷子类型 ----------
            function addGrainType(name = `谷子${grainTypes.length + 1}`, weight = 60) {
                grainTypes.push({ id: `gt${nextGrainTypeId++}`, name: name, weightPerUnit: weight });
                renderGrainTypes();
            }

            // ---------- 添加成员 ----------
            function addMember(name = `成员${members.length + 1}`) {
                members.push({
                    id: `m${nextMemberId++}`,
                    name: name,
                    grainItems: grainTypes.length > 0 ? [{ typeId: grainTypes[0].id, quantity: 1 }] : []
                });
                renderMemberTable();
                clearAmounts();
            }

            // ---------- 导出Excel（带公式） ----------
            function exportToExcel() {
                // 先计算一次确保数据最新
                calculateAndDisplay();

                const symbol = currencySymbolInput.value.trim() || '€';
                const shippingTotal = parseFloat(totalShippingInput.value) || 0;
                const totalPackagingGrams = parseFloat(totalPackagingGramsInput.value) || 0;
                const perMemberPackaging = getPerMemberPackagingGrams();
                const memberCount = members.length;

                // 创建工作簿
                const wb = XLSX.utils.book_new();

                // === Sheet 1: 谷子类型库 ===
                const grainTypeData = [
                    ['谷子类型名称', '单位克重(g)']
                ];
                grainTypes.forEach(type => {
                    grainTypeData.push([type.name, type.weightPerUnit]);
                });
                const grainTypeWS = XLSX.utils.aoa_to_sheet(grainTypeData);
                // 设置列宽
                grainTypeWS['!cols'] = [{ wch: 20 }, { wch: 15 }];
                XLSX.utils.book_append_sheet(wb, grainTypeWS, '谷子类型库');

                // === Sheet 2: 分摊明细（带公式） ===
                // 构建表头
                const headers = ['姓名'];
                // 为每位成员添加谷子列（动态）
                const maxGrainItems = Math.max(1, ...members.map(m => m.grainItems.length));
                for (let i = 0; i < maxGrainItems; i++) {
                    headers.push(`谷子类型${i + 1}`, `数量${i + 1}`, `克重${i + 1}`);
                }
                headers.push('谷子总克重(g)', '包装克重(g)', '总克重(g)', '应摊运费');

                const detailData = [headers];

                // 为谷子类型库建立一个sheet用于查找（简化：直接在公式中使用常量数组，但为了可维护，使用命名区域或者直接写死值）
                // 实际上，为了公式可编辑，我们使用VLOOKUP到谷子类型库sheet
                // 谷子类型库sheet的行：A=名称, B=克重

                // 构建每一行
                members.forEach((member, mIdx) => {
                    const row = [member.name];
                    const rowNum = mIdx + 2; // 数据行从第2行开始（第1行是表头）

                    member.grainItems.forEach((item, gIdx) => {
                        // 谷子类型列（使用VLOOKUP公式根据名称查找克重，但这里放类型名称，克重列用公式）
                        const typeName = grainTypes.find(t => t.id === item.typeId)?.name || '';
                        row.push(typeName);
                        row.push(item.quantity);

                        // 克重列使用公式：=VLOOKUP(类型名称单元格, 谷子类型库!$A$2:$B$100, 2, FALSE) * 数量单元格
                        const typeColLetter = getColumnLetter(2 + gIdx * 3); // 谷子类型列
                        const qtyColLetter = getColumnLetter(3 + gIdx * 3); // 数量列
                        const formula = `=VLOOKUP(${typeColLetter}${rowNum}, 谷子类型库!$A$2:$B$100, 2, FALSE)*${qtyColLetter}${rowNum}`;
                        row.push(formula);
                    });

                    // 如果该成员谷子项少于maxGrainItems，补空
                    for (let i = member.grainItems.length; i < maxGrainItems; i++) {
                        row.push('', '', '');
                    }

                    // 谷子总克重公式
                    const grainWeightCols = [];
                    for (let i = 0; i < maxGrainItems; i++) {
                        grainWeightCols.push(getColumnLetter(4 + i * 3)); // 克重列位置
                    }
                    const grainTotalFormula = grainWeightCols.map(col => `${col}${rowNum}`).join('+');
                    row.push(`=${grainTotalFormula}` || '0');

                    // 包装克重公式（平均分配）
                    const packagingCol = getColumnLetter(headers.length - 2);
                    row.push(`=包装总克重!$B$2/${memberCount}`);

                    // 总克重公式
                    const grainTotalCol = getColumnLetter(headers.length - 3);
                    const totalGramsCol = getColumnLetter(headers.length - 1);
                    row.push(`=${grainTotalCol}${rowNum}+${packagingCol}${rowNum}`);

                    // 应摊运费公式
                    const shippingCol = getColumnLetter(headers.length);
                    row.push(`=${totalGramsCol}${rowNum}/SUM(${totalGramsCol}$2:${totalGramsCol}$${members.length + 1})*$B$1`);

                    detailData.push(row);
                });

                // 添加汇总行
                const totalRow = ['合计'];
                // 谷子类型列留空
                for (let i = 0; i < maxGrainItems * 3; i++) {
                    totalRow.push('');
                }
                // 谷子总克重合计
                const grainTotalColHeader = getColumnLetter(headers.length - 3);
                totalRow.push(`=SUM(${grainTotalColHeader}2:${grainTotalColHeader}${members.length + 1})`);
                // 包装总克重
                totalRow.push(totalPackagingGrams);
                // 总克重合计
                const totalGramsColHeader = getColumnLetter(headers.length - 1);
                totalRow.push(`=SUM(${totalGramsColHeader}2:${totalGramsColHeader}${members.length + 1})`);
                // 应摊运费合计
                const amountColHeader = getColumnLetter(headers.length);
                totalRow.push(`=SUM(${amountColHeader}2:${amountColHeader}${members.length + 1})`);
                detailData.push(totalRow);

                const detailWS = XLSX.utils.aoa_to_sheet(detailData);
                // 设置列宽
                const detailCols = [{ wch: 12 }];
                for (let i = 0; i < maxGrainItems; i++) {
                    detailCols.push({ wch: 15 }, { wch: 8 }, { wch: 12 });
                }
                detailCols.push({ wch: 15 }, { wch: 12 }, { wch: 12 }, { wch: 15 });
                detailWS['!cols'] = detailCols;

                // 在明细sheet的A1放运费总额，方便公式引用
                // 实际我们把总运费放在B1，便于公式引用
                detailData[0].push(''); // 补充表头
                detailWS['!ref'] = XLSX.utils.encode_range({
                    s: { r: 0, c: 0 },
                    e: { r: detailData.length, c: headers.length }
                });
                // 手动设置B1为运费总额
                detailWS['B1'] = { t: 'n', v: shippingTotal };

                XLSX.utils.book_append_sheet(wb, detailWS, '分摊明细');

                // === Sheet 3: 包装总克重 ===
                const packagingData = [
                    ['包装总克重(g)', totalPackagingGrams]
                ];
                const packagingWS = XLSX.utils.aoa_to_sheet(packagingData);
                packagingWS['!cols'] = [{ wch: 20 }, { wch: 15 }];
                XLSX.utils.book_append_sheet(wb, packagingWS, '包装总克重');

                // 导出文件
                const fileName = `国际计算器_${new Date().toISOString().slice(0,10)}.xlsx`;
                XLSX.writeFile(wb, fileName);
            }

            function getColumnLetter(colNum) {
                let dividend = colNum;
                let columnName = '';
                let modulo;
                while (dividend > 0) {
                    modulo = (dividend - 1) % 26;
                    columnName = String.fromCharCode(65 + modulo) + columnName;
                    dividend = Math.floor((dividend - modulo) / 26);
                }
                return columnName;
            }

            // ---------- 初始化 ----------
            function initializeSample() {
                totalShippingInput.value = '300.00';
                totalPackagingGramsInput.value = '245';
                currencySymbolInput.value = '€';
                renderGrainTypes();
                renderMemberTable();
                calculateAndDisplay();
            }

            // ---------- 事件绑定 ----------
            addGrainTypeBtn.addEventListener('click', () => addGrainType());
            addMemberBtn.addEventListener('click', () => addMember());
            calculateBtn.addEventListener('click', calculateAndDisplay);
            exportBtn.addEventListener('click', exportToExcel);

            totalShippingInput.addEventListener('input', () => updateSummaryDisplay());
            totalPackagingGramsInput.addEventListener('input', () => {
                renderMemberTable();
                updateSummaryDisplay();
            });
            currencySymbolInput.addEventListener('input', () => {
                updateCurrencyBadges();
                updateSummaryDisplay();
            });

            window.addEventListener('DOMContentLoaded', initializeSample);
        })();
    </script>
</body>
</html>
