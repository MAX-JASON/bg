<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>家庭風險保障規劃 - 專業財務顧問分析</title>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #3498db;
            --accent: #e74c3c;
            --light: #ecf0f1;
            --dark: #2c3e50;
            --success: #2ecc71;
            --warning: #f39c12;
            --danger: #e74c3c;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft JhengHei', sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 30px 20px;
            border-radius: 10px;
            margin-bottom: 30px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            text-align: center;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.08);
            border: 1px solid rgba(52, 152, 219, 0.1);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(90deg, var(--secondary), var(--primary));
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.12);
        }
        
        .card-title {
            font-size: 1.5rem;
            color: var(--primary);
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--light);
            text-align: center;
        }

        /* 第四/五頁需要的基本樣式（精簡版） */
        .chart-container { position: relative; height: 400px; margin: 20px 0; }
        .tab-container { margin: 20px 0; }
        .tab-buttons { display: flex; flex-wrap: wrap; gap: 10px; margin-bottom: 20px; }
        .tab-button { padding: 12px 24px; background-color: var(--light); border: none; border-radius: 6px; cursor: pointer; font-size: 1rem; transition: all 0.3s ease; }
        .tab-button.active { background-color: var(--secondary); color: #fff; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        .comparison-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(280px, 1fr)); gap: 20px; margin-top: 20px; }
        .comparison-item { background: var(--light); padding: 15px; border-radius: 8px; text-align: center; }
        .comparison-value { font-size: 1.8rem; font-weight: bold; color: var(--secondary); margin: 10px 0; }
        .future-medical { display: grid; grid-template-columns: repeat(auto-fill, minmax(250px, 1fr)); gap: 20px; margin-top: 20px; }
        .future-item { background: #fff; padding: 20px; border-radius: 8px; box-shadow: 0 3px 10px rgba(0,0,0,0.08); text-align: center; }
        .future-cost { font-size: 1.5rem; font-weight: bold; color: var(--accent); margin: 10px 0; }
        .coverage-bad { color: var(--danger); }

        .section-intro {
            text-align: center;
            margin-bottom: 30px;
            color: #555;
            font-size: 1.1rem;
        }
        
        /* 頁面導航 */
        .page-navigation {
            display: flex;
            justify-content: center;
            margin-bottom: 40px;
            gap: 15px;
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.08);
        }
        
        .nav-btn {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border: 2px solid transparent;
            color: var(--primary);
            padding: 15px 30px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .nav-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            transition: left 0.3s ease;
            z-index: 1;
        }
        
        .nav-btn span {
            position: relative;
            z-index: 2;
        }
        
        .nav-btn.active {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            border-color: transparent;
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
        }
        
        .nav-btn:hover:not(.active) {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
            border-color: var(--secondary);
        }
        
        /* 頁面內容 */
        .page {
            display: none;
        }
        
        .page.active {
            display: block;
        }
        
        /* 風險意識區塊 */
        .risk-awareness {
            background: linear-gradient(135deg, #ffeaa7, #fab1a0);
            padding: 30px;
            border-radius: 10px;
            margin: 30px 0;
        }
        
        .risk-question {
            background: white;
            padding: 20px;
            border-radius: 8px;
            margin: 15px 0;
            border-left: 4px solid #e74c3c;
            cursor: pointer;
            transition: transform 0.3s;
        }
        .risk-answer {
            background: #e8f4fd;
            padding: 15px;
            border-radius: 8px;
            margin-top: 10px;
            display: none;
        }
        
        /* 人生階段比較表 */
        .life-stage-comparison {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            margin: 30px 0;
        }
        
        .stage-card {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 30px rgba(0,0,0,0.08);
            border: 1px solid rgba(52, 152, 219, 0.1);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .stage-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: linear-gradient(90deg, var(--secondary), var(--primary));
        }
        
        .stage-card.young::before { background: linear-gradient(90deg, #3498db, #2980b9); }
        .stage-card.family::before { background: linear-gradient(90deg, #9b59b6, #8e44ad); }
        .stage-card.retirement::before { background: linear-gradient(90deg, #e67e22, #d35400); }
        
        .stage-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 40px rgba(0,0,0,0.15);
        }
        
        .stage-card h3 {
            color: var(--primary);
            margin-bottom: 20px;
            text-align: center;
            font-size: 1.4rem;
            padding-bottom: 10px;
            border-bottom: 2px solid rgba(0,0,0,0.1);
        }
        
        .risk-list {
            list-style: none;
            margin: 20px 0;
        }
        
        .risk-list li {
            padding: 12px 0;
            border-bottom: 1px solid rgba(0,0,0,0.05);
            position: relative;
            padding-left: 25px;
            transition: all 0.3s ease;
        }
        
        .risk-list li::before {
            content: '•';
            position: absolute;
            left: 0;
            color: var(--secondary);
            font-weight: bold;
            font-size: 1.2rem;
        }
        
        .risk-list li:hover {
            background: rgba(52, 152, 219, 0.05);
            padding-left: 30px;
            border-radius: 5px;
        }
        
        .solution-list {
            background: linear-gradient(135deg, #e8f6f3, #d1f2eb);
            padding: 20px;
            border-radius: 10px;
            margin-top: 20px;
            border-left: 4px solid #27ae60;
            box-shadow: 0 4px 15px rgba(39, 174, 96, 0.1);
        }
        
        .solution-list li {
            padding: 8px 0;
            color: #27ae60;
            position: relative;
            padding-left: 25px;
        }
        
        .solution-list li::before {
            content: '✓';
            position: absolute;
            left: 0;
            color: #27ae60;
            font-weight: bold;
        }
        
        /* 問題解決框架 */
        .problem-solution-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin: 30px 0;
        }
        
        .problem-column, .solution-column {
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.08);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .problem-column::before, .solution-column::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
        }
        
        .problem-column {
            border-left: 4px solid #e74c3c;
            background: linear-gradient(135deg, #fff, #fef2f2);
        }
        
        .problem-column::before {
            background: linear-gradient(90deg, #e74c3c, #c0392b);
        }
        
        .solution-column {
            border-left: 4px solid #27ae60;
            background: linear-gradient(135deg, #fff, #f0f9ff);
        }
        
        .solution-column::before {
            background: linear-gradient(90deg, #27ae60, #2ecc71);
        }
        
        .problem-column:hover, .solution-column:hover {
            transform: translateY(-3px);
            box-shadow: 0 12px 35px rgba(0,0,0,0.12);
        }
        
        .problem-column h3, .solution-column h3 {
            color: var(--primary);
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid rgba(0,0,0,0.1);
            text-align: center;
        }
        
        /* 表單樣式 */
        .input-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        .form-label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--primary);
            transition: all 0.3s ease;
            position: relative;
            padding-left: 8px;
        }
        
        .form-label::before {
            content: '';
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 3px;
            height: 16px;
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            border-radius: 2px;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .form-group:focus-within .form-label::before {
            opacity: 1;
        }
        
        .form-input {
            width: 100%;
            padding: 14px 16px;
            border: 2px solid #e1e8ed;
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s ease;
            background: #fafbfc;
            box-shadow: 0 2px 4px rgba(0,0,0,0.04);
        }
        
        .form-input:focus {
            border-color: var(--secondary);
            background: white;
            box-shadow: 0 4px 12px rgba(52, 152, 219, 0.15);
            transform: translateY(-1px);
            outline: none;
        }
        
        .form-input:hover {
            border-color: #c8d6e5;
            background: white;
        }
        
        .submit-btn {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            border: none;
            padding: 18px 40px;
            border-radius: 12px;
            font-size: 1.2rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.4s ease;
            margin-top: 20px;
            width: 100%;
            box-shadow: 0 6px 20px rgba(52, 152, 219, 0.3);
            position: relative;
            overflow: hidden;
        }
        
        .submit-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            transition: left 0.4s ease;
            z-index: 1;
        }
        
        .submit-btn span {
            position: relative;
            z-index: 2;
        }
        
        .submit-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 30px rgba(52, 152, 219, 0.4);
        }
        
        .submit-btn:hover::before {
            left: 0;
        }
        
        .submit-btn:active {
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
        }

        /* 評估結果樣式 */
        .evaluation-result {
            background: white;
            padding: 25px;
            border-radius: 12px;
            margin: 20px 0;
            box-shadow: 0 6px 20px rgba(0,0,0,0.08);
            border: 1px solid rgba(52, 152, 219, 0.1);
            transition: all 0.3s ease;
        }
        
        .evaluation-result:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.12);
        }
        
        .checkmark {
            color: var(--success);
            font-weight: bold;
            background: rgba(46, 204, 113, 0.1);
            padding: 2px 8px;
            border-radius: 4px;
            margin-right: 5px;
        }
        
        .crossmark {
            color: var(--danger);
            font-weight: bold;
            background: rgba(231, 76, 60, 0.1);
            padding: 2px 8px;
            border-radius: 4px;
            margin-right: 5px;
        }

        /* 第二頁風險輪廓與充足度 */
        .risk-grid { display: grid; grid-template-columns: 1.2fr 1fr; gap: 20px; margin-bottom: 20px; }
        .risk-card { background: #fff; border-radius: 12px; padding: 20px; box-shadow: 0 6px 18px rgba(0,0,0,0.06); }
        .risk-bullets { list-style: none; margin: 10px 0 0; padding: 0; }
        .risk-bullets li { padding: 8px 10px; border-left: 4px solid var(--secondary); background: #f7fbff; border-radius: 6px; margin-bottom: 8px; }
        .kpi-tip { color: #6b7280; font-size: 0.9rem; margin-top: 10px; }
        .mini-kpi { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-top: 12px; }
        .kpi-label { color: #6b7280; margin-right: 8px; }
        .kpi-value { font-weight: 700; color: var(--primary); }
        .adequacy-list { display: grid; grid-template-columns: 1fr; gap: 12px; margin-top: 10px; }
        .adequacy-row { display: grid; grid-template-columns: 160px 1fr 90px; gap: 12px; align-items: center; }
        .adequacy-bar { height: 12px; background: #ecf0f1; border-radius: 8px; overflow: hidden; position: relative; }
        .adequacy-bar > span { display: block; height: 100%; background: linear-gradient(90deg, #6dd5ed, #2193b0); }
        .adequacy-status { text-align: right; font-weight: 600; }
        .adequacy-ok { color: var(--success); }
        .adequacy-warn { color: var(--warning); }
        .gap-box { background: #fff; border: 1px solid #eef2f7; border-radius: 10px; padding: 12px 16px; margin-top: 14px; }
        .gap-box h4 { margin-bottom: 8px; }
        .gap-box ul { margin: 0; padding-left: 18px; }
        .note { color: #6b7280; }

        /* 第三頁方案總覽 */
        .solution-tracks { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 16px; margin-top: 12px; }
        .solution-track { background: #fff; border: 1px solid #eef2f7; border-radius: 12px; padding: 14px 16px; }
        .solution-track h3 { margin-bottom: 8px; }
        .solution-track ul { margin: 0; padding-left: 18px; }
        .gap-summary { background: #fff; border: 1px dashed #cfe5ff; border-radius: 12px; padding: 12px 16px; margin-top: 16px; }

        /* 第四頁圖區雙欄 */
        .chart-grid { display: grid; grid-template-columns: 2fr 1.2fr; gap: 16px; }
        @media (max-width: 900px){ .chart-grid { grid-template-columns: 1fr; } }

        /* 第五頁未來趨勢與規劃 */
        .nhi-trend-section {
            background: linear-gradient(135deg, #fff 0%, #f0f9ff 100%);
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 30px;
        }

        .trend-highlights {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .trend-card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            border-left: 4px solid;
            display: flex;
            gap: 15px;
        }

        .trend-warning { border-left-color: #f39c12; }
        .trend-danger { border-left-color: #e74c3c; }
        .trend-info { border-left-color: #3498db; }

        .trend-icon {
            font-size: 2.5rem;
            flex-shrink: 0;
        }

        .trend-card h4 {
            color: var(--primary);
            margin-bottom: 8px;
            font-size: 1.1rem;
        }

        .trend-card p {
            color: #6b7280;
            font-size: 0.95rem;
            line-height: 1.5;
        }

        .treatment-comparison-section {
            margin-top: 30px;
        }

        .treatment-table-wrapper {
            overflow-x: auto;
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            margin-top: 20px;
        }

        .treatment-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.95rem;
        }

        .treatment-table th {
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
        }

        .treatment-table td {
            padding: 15px;
            border-bottom: 1px solid #f0f0f0;
        }

        .treatment-table tbody tr:hover {
            background: #f8f9fa;
        }

        .cost-high {
            color: #e74c3c;
            font-weight: 600;
        }

        .cost-medium {
            color: #f39c12;
            font-weight: 600;
        }

        .ratio-high {
            color: #e74c3c;
            font-weight: 700;
            font-size: 1.1rem;
        }

        .ratio-medium {
            color: #f39c12;
            font-weight: 700;
            font-size: 1.1rem;
        }

        .status-no {
            background: #ffe0e0;
            color: #e74c3c;
            padding: 4px 10px;
            border-radius: 6px;
            font-weight: 600;
        }

        .status-partial {
            background: #fff3cd;
            color: #f39c12;
            padding: 4px 10px;
            border-radius: 6px;
            font-weight: 600;
        }

        .timeline-planning-section {
            margin-top: 30px;
            background: linear-gradient(135deg, #f8f9ff 0%, #fff 100%);
            padding: 25px;
            border-radius: 12px;
        }

        .timeline-wrapper {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }

        .timeline-item {
            background: white;
            border-radius: 12px;
            padding: 25px;
            box-shadow: 0 6px 20px rgba(0,0,0,0.1);
            border-top: 5px solid;
            position: relative;
        }

        .timeline-phase1 { border-top-color: #3498db; }
        .timeline-phase2 { border-top-color: #9b59b6; }
        .timeline-phase3 { border-top-color: #e67e22; }

        .timeline-badge {
            position: absolute;
            top: -12px;
            left: 20px;
            background: var(--secondary);
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.9rem;
        }

        .timeline-phase2 .timeline-badge { background: #9b59b6; }
        .timeline-phase3 .timeline-badge { background: #e67e22; }

        .timeline-content h4 {
            color: var(--primary);
            margin: 15px 0 12px;
            font-size: 1.2rem;
        }

        .timeline-content ul {
            list-style: none;
            padding: 0;
            margin: 0 0 15px;
        }

        .timeline-content li {
            padding: 8px 0 8px 25px;
            position: relative;
            color: #495057;
            font-size: 0.95rem;
        }

        .timeline-content li::before {
            content: '✓';
            position: absolute;
            left: 0;
            color: #2ecc71;
            font-weight: bold;
        }

        .timeline-budget {
            background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%);
            padding: 12px;
            border-radius: 8px;
            text-align: center;
            color: #2e7d32;
        }

        .timeline-budget strong {
            font-size: 1.3rem;
            color: #1b5e20;
        }

        .inflation-calculator {
            margin-top: 30px;
            background: linear-gradient(135deg, #fff5f5 0%, #fff 100%);
            border: 2px solid #ffe0e0;
            border-radius: 12px;
            padding: 25px;
        }

        .inflation-controls {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin: 20px 0;
        }

        .inflation-controls label {
            display: flex;
            flex-direction: column;
            gap: 10px;
            font-weight: 600;
            color: var(--primary);
        }

        .inflation-controls input[type="range"] {
            width: 100%;
            height: 8px;
            border-radius: 5px;
            background: #e1e8ed;
            outline: none;
        }

        .inflation-controls span {
            font-size: 1.2rem;
            color: var(--secondary);
        }

        .inflation-result {
            margin-top: 20px;
        }

        .inflation-card {
            background: white;
            padding: 30px;
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0,0,0,0.1);
            text-align: center;
        }

        .inflation-card h4 {
            color: var(--primary);
            margin: 10px 0;
            font-size: 1.2rem;
        }

        .inflation-arrow {
            font-size: 2rem;
            margin: 15px 0;
        }

        .inflation-value {
            font-size: 3rem;
            font-weight: bold;
            color: #e74c3c;
            margin: 20px 0;
        }

        .inflation-note {
            color: #856404;
            background: #fff3cd;
            padding: 12px;
            border-radius: 8px;
            margin-top: 15px;
        }

        .future-chart-section {
            margin-top: 30px;
        }
        
        /* 第二頁風險診斷與缺口分析 */
        .section-subtitle {
            font-size: 1.3rem;
            color: var(--primary);
            margin: 30px 0 20px;
            padding-left: 15px;
            border-left: 4px solid var(--secondary);
        }

        .risk-visualization-section {
            background: linear-gradient(135deg, #f8f9ff 0%, #fff 100%);
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 30px;
        }

        .risk-dashboard {
            display: grid;
            grid-template-columns: 1.2fr 1fr;
            gap: 25px;
            margin-bottom: 20px;
        }

        .radar-container {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            height: 400px;
            display: flex;
            flex-direction: column;
        }

        .radar-container canvas {
            max-height: 300px;
        }

        .chart-note {
            text-align: center;
            color: #6b7280;
            font-size: 0.9rem;
            margin-top: 10px;
        }

        .risk-stats-cards {
            display: grid;
            grid-template-columns: 1fr;
            gap: 15px;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            display: grid;
            grid-template-columns: 50px 1fr;
            gap: 15px;
            align-items: center;
            transition: transform 0.3s ease;
            border-left: 4px solid;
        }

        .stat-card:hover {
            transform: translateX(5px);
        }

        .stat-card-critical { border-left-color: #e74c3c; }
        .stat-card-cost { border-left-color: #f39c12; }
        .stat-card-care { border-left-color: #3498db; }

        .stat-icon {
            font-size: 2.5rem;
            grid-row: 1 / 4;
        }

        .stat-label {
            font-size: 0.9rem;
            color: #6b7280;
            grid-column: 2;
        }

        .stat-value {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--primary);
            grid-column: 2;
        }

        .stat-desc {
            font-size: 0.85rem;
            color: #9ca3af;
            grid-column: 2;
        }

        .scenario-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }

        .scenario-card {
            background: white;
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 6px 20px rgba(0,0,0,0.1);
            text-align: center;
            border-top: 5px solid;
            transition: all 0.3s ease;
        }

        .scenario-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }

        .scenario-cancer { border-top-color: #e74c3c; }
        .scenario-accident { border-top-color: #f39c12; }
        .scenario-critical { border-top-color: #9b59b6; }

        .scenario-icon {
            font-size: 3rem;
            margin-bottom: 10px;
        }

        .scenario-card h5 {
            font-size: 1.2rem;
            color: var(--primary);
            margin-bottom: 15px;
        }

        .scenario-cost {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--accent);
            margin: 15px 0;
        }

        .scenario-cost span {
            color: #e74c3c;
        }

        .scenario-impact {
            background: #fff3cd;
            padding: 10px;
            border-radius: 8px;
            color: #856404;
            font-weight: 600;
            margin-top: 15px;
        }

        .coverage-gap-section {
            background: white;
            padding: 25px;
            border-radius: 12px;
        }

        .gap-dashboard {
            display: grid;
            grid-template-columns: 350px 1fr;
            gap: 30px;
            margin-bottom: 25px;
        }

        .gauge-container {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 25px;
            border-radius: 12px;
            color: white;
            text-align: center;
            box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
        }

        .gauge-title {
            font-size: 1.1rem;
            margin-bottom: 20px;
            opacity: 0.95;
        }

        .gauge-score {
            font-size: 3.5rem;
            font-weight: bold;
            margin: 15px 0 5px;
        }

        .gauge-rating {
            font-size: 1.2rem;
            opacity: 0.9;
            margin-bottom: 20px;
        }

        .gauge-legend {
            display: flex;
            justify-content: center;
            gap: 15px;
            font-size: 0.85rem;
            flex-wrap: wrap;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .legend-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            display: inline-block;
        }

        .legend-red { background: #e74c3c; }
        .legend-yellow { background: #f39c12; }
        .legend-green { background: #2ecc71; }

        .gap-bars-container {
            display: grid;
            grid-template-columns: 1fr;
            gap: 20px;
        }

        .gap-bar-item {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            transition: background 0.3s ease;
        }

        .gap-bar-item:hover {
            background: #e9ecef;
        }

        .gap-bar-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .gap-label {
            font-weight: 600;
            color: var(--primary);
            font-size: 1rem;
        }

        .gap-status {
            font-size: 0.9rem;
            font-weight: 600;
        }

        .gap-bar-visual {
            display: grid;
            gap: 8px;
        }

        .gap-bar-bg {
            position: relative;
            height: 24px;
            background: #e1e8ed;
            border-radius: 12px;
            overflow: hidden;
        }

        .gap-bar-fill {
            position: absolute;
            height: 100%;
            background: linear-gradient(90deg, #f39c12, #e67e22);
            border-radius: 12px;
            transition: width 0.8s ease;
        }

        .gap-bar-fill.gap-bar-ok {
            background: linear-gradient(90deg, #2ecc71, #27ae60);
        }

        .gap-bar-fill.gap-bar-danger {
            background: linear-gradient(90deg, #e74c3c, #c0392b);
        }

        .gap-bar-target {
            position: absolute;
            right: 0;
            top: 0;
            width: 2px;
            height: 100%;
            background: #2c3e50;
        }

        .gap-bar-numbers {
            display: flex;
            justify-content: space-between;
            font-size: 0.9rem;
            color: #495057;
        }

        .gap-diff {
            font-weight: 600;
            color: #f39c12;
        }

        .gap-diff.gap-ok {
            color: #2ecc71;
        }

        .gap-diff.gap-danger {
            color: #e74c3c;
        }

        .financial-impact-box {
            background: linear-gradient(135deg, #fff5f5 0%, #fff 100%);
            border: 2px solid #ffe0e0;
            border-radius: 12px;
            padding: 25px;
            margin-top: 20px;
        }

        .financial-impact-box h4 {
            color: var(--primary);
            margin-bottom: 20px;
            font-size: 1.2rem;
        }

        .impact-calc {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }

        .impact-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #f0f0f0;
        }

        .impact-row:last-child {
            border-bottom: none;
        }

        .impact-label {
            color: #6b7280;
            font-size: 1rem;
        }

        .impact-value {
            font-weight: 600;
            color: var(--primary);
            font-size: 1.1rem;
        }

        .impact-insurance {
            color: #2ecc71;
        }

        .impact-danger {
            color: #e74c3c;
            font-size: 1.5rem;
        }

        .impact-total {
            background: #fff3cd;
            margin: 10px -20px -20px;
            padding: 15px 20px;
            border-radius: 0 0 10px 10px;
        }

        .impact-note {
            text-align: center;
            margin-top: 15px;
            color: #856404;
            font-weight: 600;
            font-size: 1.05rem;
        }

        .impact-note span {
            color: #e74c3c;
            font-size: 1.2rem;
        }

        @media (max-width: 1024px) {
            .risk-dashboard {
                grid-template-columns: 1fr;
            }
            .gap-dashboard {
                grid-template-columns: 1fr;
            }
        }

        /* 第三頁解決方案 */
        .priority-classification {
            background: linear-gradient(135deg, #fff 0%, #f8f9ff 100%);
            padding: 25px;
            border-radius: 12px;
            margin-bottom: 30px;
        }

        .priority-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }

        .priority-box {
            background: white;
            border-radius: 12px;
            padding: 20px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
            border-left: 5px solid;
        }

        .priority-critical { border-left-color: #e74c3c; }
        .priority-medium { border-left-color: #f39c12; }
        .priority-low { border-left-color: #2ecc71; }

        .priority-header {
            display: flex;
            align-items: center;
            gap: 10px;
            margin-bottom: 15px;
        }

        .priority-icon {
            font-size: 1.5rem;
        }

        .priority-header h4 {
            font-size: 1.1rem;
            color: var(--primary);
            margin: 0;
        }

        .priority-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .priority-list li {
            padding: 10px;
            background: #f8f9fa;
            border-radius: 6px;
            margin-bottom: 8px;
            font-size: 0.95rem;
            color: #495057;
        }

        .solution-plans {
            margin-top: 30px;
        }

        .plans-comparison {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 25px;
            margin-top: 20px;
        }

        .plan-card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
            border: 3px solid;
            position: relative;
            transition: all 0.3s ease;
        }

        .plan-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 12px 35px rgba(0,0,0,0.15);
        }

        .plan-basic { border-color: #3498db; }
        .plan-complete { border-color: #2ecc71; }
        .plan-premium { border-color: #9b59b6; }

        .plan-badge {
            position: absolute;
            top: -12px;
            left: 20px;
            background: #3498db;
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-weight: 600;
            font-size: 0.9rem;
        }

        .plan-complete .plan-badge {
            background: #2ecc71;
        }

        .plan-premium .plan-badge {
            background: #9b59b6;
        }

        .plan-badge-recommended {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%) !important;
            padding: 5px 20px;
        }

        .plan-title {
            font-size: 1.5rem;
            color: var(--primary);
            margin: 20px 0 15px;
            text-align: center;
        }

        .plan-price {
            text-align: center;
            margin: 20px 0;
        }

        .price-amount {
            font-size: 2.5rem;
            font-weight: bold;
            color: var(--secondary);
        }

        .price-unit {
            font-size: 1rem;
            color: #6b7280;
            margin-left: 5px;
        }

        .plan-desc {
            text-align: center;
            color: #6b7280;
            margin-bottom: 20px;
            font-size: 0.95rem;
            min-height: 40px;
        }

        .plan-coverage {
            margin: 25px 0;
        }

        .plan-coverage h5 {
            color: var(--primary);
            margin-bottom: 12px;
            font-size: 1rem;
        }

        .plan-list {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .plan-list li {
            padding: 8px 0;
            border-bottom: 1px solid #f0f0f0;
            font-size: 0.95rem;
            color: #495057;
        }

        .plan-list li:last-child {
            border-bottom: none;
        }

        .plan-list .check {
            color: #2ecc71;
            margin-right: 8px;
            font-weight: bold;
        }

        .plan-result {
            background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%);
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            margin: 20px 0;
        }

        .result-score {
            font-size: 2rem;
            font-weight: bold;
            color: #2ecc71;
            margin: 0 10px;
        }

        .result-label {
            display: block;
            font-size: 0.9rem;
            color: #6b7280;
            margin-top: 5px;
        }

        .result-excellent {
            color: #2ecc71;
            font-weight: 600;
        }

        .plan-checkbox {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
            cursor: pointer;
            transition: background 0.3s ease;
            font-weight: 600;
        }

        .plan-checkbox:hover {
            background: #e9ecef;
        }

        .plan-checkbox input[type="checkbox"] {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }

        .affordability-check {
            background: linear-gradient(135deg, #fff3cd 0%, #fff 100%);
            border: 2px solid #ffc107;
            border-radius: 12px;
            padding: 25px;
            margin-top: 30px;
        }

        .affordability-check h4 {
            color: var(--primary);
            margin-bottom: 20px;
            font-size: 1.2rem;
        }

        .affordability-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .affordability-item {
            background: white;
            padding: 15px;
            border-radius: 10px;
            display: flex;
            flex-direction: column;
            gap: 8px;
        }

        .afford-label {
            color: #6b7280;
            font-size: 0.9rem;
        }

        .afford-value {
            font-size: 1.3rem;
            font-weight: bold;
            color: var(--primary);
        }

        .afford-status {
            font-size: 1.1rem;
            font-weight: 600;
            color: #2ecc71;
        }

        .afford-note {
            text-align: center;
            margin-top: 15px;
            color: #856404;
            font-size: 0.95rem;
        }

        /* 第三頁選項卡 */
        .tab-navigation {
            display: flex;
            justify-content: center;
            margin-bottom: 30px;
            gap: 15px;
            background: white;
            padding: 20px;
            border-radius: 15px;
            box-shadow: 0 4px 20px rgba(0,0,0,0.08);
        }
        
        .tab-btn {
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border: 2px solid transparent;
            color: var(--primary);
            padding: 15px 30px;
            border-radius: 12px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        
        .tab-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            transition: left 0.3s ease;
            z-index: 1;
        }
        
        .tab-btn span {
            position: relative;
            z-index: 2;
        }
        
        .tab-btn.active {
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            color: white;
            border-color: transparent;
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
        }
        
        .tab-btn:hover:not(.active) {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
            border-color: var(--secondary);
        }
        
        .tab-content {
            display: none;
        }
        
        .tab-content.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        /* 動畫效果 */
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }
        
        .pulse-animation {
            animation: pulse 2s infinite;
        }
        
        /* 響應式設計 */
        @media (max-width: 768px) {
            .problem-solution-grid {
                grid-template-columns: 1fr;
            }
            
            .life-stage-comparison {
                grid-template-columns: 1fr;
            }
            
            .page-navigation, .tab-navigation {
                flex-wrap: wrap;
            }
            
            .stage-card {
                padding: 20px;
            }
            
            .card {
                padding: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>家庭風險保障規劃</h1>
            <p class="subtitle">從「被動買保單」到「主動規劃人生」的專業轉變</p>
        </header>

        <!-- 頁面導航 -->
        <div class="page-navigation">
            <button class="nav-btn active" onclick="showPage(1)">第一頁：客戶資訊</button>
            <button class="nav-btn" onclick="showPage(2)">第二頁：保障分析</button>
            <button class="nav-btn" onclick="showPage(3)">第三頁：解決方案</button>
            <button class="nav-btn" onclick="showPage(4)">第四頁：醫療費用對比</button>
            <button class="nav-btn" onclick="showPage(5)">第五頁：未來醫療趨勢</button>
        </div>

        <!-- 第一頁：客戶資訊輸入 -->
        <div id="page1" class="page active">
            <section class="card">
                <h2 class="card-title">📝 客戶資訊輸入</h2>
                <div class="section-intro">
                    請輸入客戶基本資訊，我們將為您生成專業的保障分析報告
                </div>
                
                <!-- 輸入表單 -->
                <div class="input-section">
                    <form id="insuranceForm">
                        <div class="input-form">
                            <div>
                                <div class="form-group">
                                    <label class="form-label">客戶姓名</label>
                                    <input type="text" class="form-input" id="clientName" value="屈伸儀">
                                </div>
                                <div class="form-group">
                                    <label class="form-label">年齡</label>
                                    <input type="number" class="form-input" id="clientAge" value="40" min="20" max="80">
                                    <small id="hint-age">用於判斷人生階段</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">家庭月收入（萬元）</label>
                                    <input type="number" class="form-input" id="monthlyIncome" value="8" step="0.5">
                                    <small id="hint-monthly">用於評估合理保費負擔</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">年收入（萬元）</label>
                                    <input type="number" class="form-input" id="annualIncome" value="96" step="10">
                                    <small id="hint-annual">可留空，系統會以月收入×12 推算</small>
                                </div>
                            </div>
                            <div>
                                <div class="form-group">
                                    <label class="form-label">一般身故保障（萬元）</label>
                                    <input type="number" class="form-input" id="deathBenefit" value="300" step="1">
                                    <small id="hint-death">理想建議：<span data-ideal="death">600</span> 萬（<50歲）</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">意外身故保障（萬元）</label>
                                    <input type="number" class="form-input" id="accidentDeath" value="600" step="1">
                                    <small id="hint-accident">理想建議：<span data-ideal="accidentalDeath">600</span> 萬</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">實支實付限額（萬元）</label>
                                    <input type="number" class="form-input" id="medicalLimit" value="20" step="1">
                                    <small id="hint-medical">理想建議：<span data-ideal="reimbursement">30</span> 萬（新式治療）</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">重大疾病一次金（萬元）</label>
                                    <input type="number" class="form-input" id="criticalIllness" value="100" step="1">
                                    <small id="hint-critical">理想建議：<span data-ideal="criticalIllness">100</span> 萬</small>
                                </div>
                            </div>
                            <div>
                                <div class="form-group">
                                    <label class="form-label">癌症險一次金（萬元）</label>
                                    <input type="number" class="form-input" id="cancerBenefit" value="50" step="1">
                                    <small id="hint-cancer">理想建議：<span data-ideal="cancer">100</span> 萬</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">手術險最高給付（萬元）</label>
                                    <input type="number" class="form-input" id="surgeryBenefit" value="16" step="1">
                                    <small id="hint-surgery">理想建議：<span data-ideal="surgery">16</span> 萬</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">意外住院日額（元）</label>
                                    <input type="number" class="form-input" id="accidentalHospital" value="6500">
                                    <small id="hint-accHos">理想建議：<span data-ideal="accidentalHospital">3000</span> 元/日</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">疾病住院日額（元）</label>
                                    <input type="number" class="form-input" id="illnessHospital" value="5000">
                                    <small id="hint-illHos">理想建議：<span data-ideal="illnessHospital">3000</span> 元/日</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">失能險月領（萬元/月）</label>
                                    <input type="number" class="form-input" id="disability" value="0.9" step="0.1">
                                    <small id="hint-disability">理想：收入替代率 ≥60%</small>
                                </div>
                                <div class="form-group">
                                    <label class="form-label">長照險月給付（萬元/月）</label>
                                    <input type="number" class="form-input" id="longTermCare" value="0" step="0.1">
                                    <small id="hint-ltc">理想建議：<span data-ideal="longTermCare">4.5</span> 萬/月</small>
                                </div>
                            </div>
                        </div>
                        <button type="button" class="submit-btn" onclick="generateAnalysis()">
                            🚀 生成專業保障規劃報告
                        </button>
                        <button type="button" class="submit-btn" onclick="downloadProposal()" style="background: linear-gradient(135deg, #27ae60, #229954); margin-top: 10px;">
                            📄 下載客戶建議書 (PDF)
                        </button>
                    </form>
                </div>
            </section>
        </div>

        <!-- 第二頁：保障分析 -->
        <div id="page2" class="page">
            <section class="card">
                <h2 class="card-title">📊 風險診斷與保障缺口分析</h2>
                
                <!-- 🆕 快速診斷卡（3秒看重點） -->
                <div class="quick-diagnosis" id="quickDiagnosis" style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 25px; border-radius: 15px; margin-bottom: 30px; box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);">
                    <h3 style="margin: 0 0 20px; font-size: 1.4rem; display: flex; align-items: center; gap: 10px;">
                        <span style="font-size: 1.8rem;">⚡</span> 3秒快速診斷
                    </h3>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                        <div style="background: rgba(255,255,255,0.15); padding: 15px; border-radius: 10px; backdrop-filter: blur(10px);">
                            <div style="font-size: 0.9rem; opacity: 0.9; margin-bottom: 5px;">風險評分</div>
                            <div style="font-size: 2rem; font-weight: bold;" id="quickRiskScore">68</div>
                            <div style="font-size: 0.85rem; margin-top: 5px;" id="quickRiskLevel">中高風險</div>
                        </div>
                        <div style="background: rgba(255,255,255,0.15); padding: 15px; border-radius: 10px; backdrop-filter: blur(10px);">
                            <div style="font-size: 0.9rem; opacity: 0.9; margin-bottom: 5px;">最大缺口</div>
                            <div style="font-size: 1.5rem; font-weight: bold; color: #fff59d;" id="quickMaxGap">壽險 300萬</div>
                            <div style="font-size: 0.85rem; margin-top: 5px;">達成率 50%</div>
                        </div>
                        <div style="background: rgba(255,255,255,0.15); padding: 15px; border-radius: 10px; backdrop-filter: blur(10px);">
                            <div style="font-size: 0.9rem; opacity: 0.9; margin-bottom: 5px;">缺口項目</div>
                            <div style="font-size: 2rem; font-weight: bold;" id="quickGapCount">4</div>
                            <div style="font-size: 0.85rem; margin-top: 5px;">項需補強</div>
                        </div>
                        <div style="background: rgba(255,255,255,0.15); padding: 15px; border-radius: 10px; backdrop-filter: blur(10px);">
                            <div style="font-size: 0.9rem; opacity: 0.9; margin-bottom: 5px;">建議優先級</div>
                            <div style="font-size: 1.2rem; font-weight: bold;" id="quickPriority">P0: 2項</div>
                            <div style="font-size: 0.85rem; margin-top: 5px;">P1: 2項</div>
                        </div>
                    </div>
                    <div style="margin-top: 20px; padding: 15px; background: rgba(255,255,255,0.2); border-radius: 8px; border-left: 4px solid #fff59d;">
                        <div style="font-size: 0.95rem; font-weight: 600; margin-bottom: 8px;">⚠️ 核心建議：</div>
                        <div id="quickRecommendation" style="font-size: 0.9rem; line-height: 1.6;">
                            優先處理壽險不足和癌症險缺口，可降低 80% 風險
                        </div>
                    </div>
                </div>
                
                <div class="section-intro" id="emotionalIntro">
                    <!-- 動態顯示情感引導文字 -->
                </div>
                
                <!-- 風險意識喚醒區 -->
                <div class="risk-awareness" id="riskAwareness" style="margin-bottom: 30px;">
                    <!-- 動態生成風險場景化描述 -->
                </div>

                <!-- 上半部：風險具體化 -->
                <div class="risk-visualization-section">
                    <h3 class="section-subtitle">🎯 您這個年齡層的風險全景</h3>
                    
                    <div class="risk-dashboard">
                        <!-- 左側：風險雷達圖 -->
                        <div class="radar-container">
                            <canvas id="riskRadarChart"></canvas>
                            <p class="chart-note">說明：分數代表該年齡段各風險類別的相對發生機率（0-100）</p>
                        </div>

                        <!-- 右側：真實數據卡片 -->
                        <div class="risk-stats-cards">
                            <div class="stat-card stat-card-critical">
                                <div class="stat-icon">🏥</div>
                                <div class="stat-label">重大疾病發生率</div>
                                <div class="stat-value" id="criticalRate">8%</div>
                                <div class="stat-desc">每100人中有8人</div>
                            </div>
                            <div class="stat-card stat-card-cost">
                                <div class="stat-icon">💰</div>
                                <div class="stat-label">平均醫療自費</div>
                                <div class="stat-value" id="avgSelfPay">45萬</div>
                                <div class="stat-desc">重症治療平均費用</div>
                            </div>
                            <div class="stat-card stat-card-care">
                                <div class="stat-icon">🛡️</div>
                                <div class="stat-label">失能照護時長</div>
                                <div class="stat-value" id="careYears">7.3年</div>
                                <div class="stat-desc">平均照護需求</div>
                            </div>
                        </div>
                    </div>

                    <!-- 情境模擬卡片 -->
                    <div class="scenario-cards">
                        <h4 style="text-align:center; margin: 30px 0 15px; color: var(--primary); font-size: 1.2rem;">💥 如果明天發生，您準備好了嗎？</h4>
                        <div class="scenario-grid">
                            <div class="scenario-card scenario-cancer">
                                <div class="scenario-icon">🎗️</div>
                                <h5>癌症治療</h5>
                                <div class="scenario-cost">需準備 <span id="scenarioCancerCost">100萬</span></div>
                                <p>標靶/免疫療法</p>
                                <div class="scenario-impact" id="scenarioCancerImpact">自費缺口：46萬</div>
                            </div>
                            <div class="scenario-card scenario-accident">
                                <div class="scenario-icon">🚑</div>
                                <h5>意外失能</h5>
                                <div class="scenario-cost">每月損失 <span id="scenarioAccidentCost">8萬</span></div>
                                <p>收入中斷 + 照護費</p>
                                <div class="scenario-impact" id="scenarioAccidentImpact">月缺口：7.1萬</div>
                            </div>
                            <div class="scenario-card scenario-critical">
                                <div class="scenario-icon">🏥</div>
                                <h5>突發重症</h5>
                                <div class="scenario-cost">需準備 <span id="scenarioCriticalCost">120萬</span></div>
                                <p>ICU + 手術 + 復健</p>
                                <div class="scenario-impact" id="scenarioCriticalImpact">自費缺口：50萬</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 下半部：保障缺口診斷儀表板 -->
                <div class="coverage-gap-section">
                    <h3 class="section-subtitle">🔍 您的保障缺口診斷</h3>
                    
                    <div class="gap-dashboard">
                        <!-- 左側：總分儀表盤 -->
                        <div class="gauge-container">
                            <div class="gauge-title">保障充足度總分</div>
                            <canvas id="gaugeChart" width="280" height="200"></canvas>
                            <div class="gauge-score" id="totalScore">65</div>
                            <div class="gauge-rating" id="scoreRating">需要改善</div>
                            <div class="gauge-legend">
                                <span class="legend-item"><span class="legend-dot legend-red"></span>0-60 高風險</span>
                                <span class="legend-item"><span class="legend-dot legend-yellow"></span>61-80 待改善</span>
                                <span class="legend-item"><span class="legend-dot legend-green"></span>81-100 良好</span>
                            </div>
                        </div>

                        <!-- 右側：各險種缺口視覺化 -->
                        <div class="gap-bars-container">
                            <div class="gap-bar-item">
                                <div class="gap-bar-header">
                                    <span class="gap-label">壽險保障</span>
                                    <span class="gap-percent" id="percentDeath" style="font-weight: bold; color: #667eea;">50%</span>
                                    <span class="gap-status" id="statusDeath">⚠️ 不足</span>
                                </div>
                                <div class="gap-bar-visual">
                                    <div class="gap-bar-bg">
                                        <div class="gap-bar-fill" id="barDeath" style="width: 50%"></div>
                                        <div class="gap-bar-target"></div>
                                    </div>
                                    <div class="gap-bar-numbers">
                                        <span id="numDeath">300萬 / 600萬</span>
                                        <span class="gap-diff" id="diffDeath">缺300萬</span>
                                    </div>
                                </div>
                            </div>

                            <div class="gap-bar-item">
                                <div class="gap-bar-header">
                                    <span class="gap-label">意外保障</span>
                                    <span class="gap-percent" id="percentAccident" style="font-weight: bold; color: #667eea;">100%</span>
                                    <span class="gap-status" id="statusAccident">✅ 足夠</span>
                                </div>
                                <div class="gap-bar-visual">
                                    <div class="gap-bar-bg">
                                        <div class="gap-bar-fill gap-bar-ok" id="barAccident" style="width: 100%"></div>
                                        <div class="gap-bar-target"></div>
                                    </div>
                                    <div class="gap-bar-numbers">
                                        <span id="numAccident">600萬 / 600萬</span>
                                        <span class="gap-diff gap-ok" id="diffAccident">達標</span>
                                    </div>
                                </div>
                            </div>

                            <div class="gap-bar-item">
                                <div class="gap-bar-header">
                                    <span class="gap-label">實支實付</span>
                                    <span class="gap-percent" id="percentMedical" style="font-weight: bold; color: #667eea;">67%</span>
                                    <span class="gap-status" id="statusMedical">⚠️ 不足</span>
                                </div>
                                <div class="gap-bar-visual">
                                    <div class="gap-bar-bg">
                                        <div class="gap-bar-fill" id="barMedical" style="width: 67%"></div>
                                        <div class="gap-bar-target"></div>
                                    </div>
                                    <div class="gap-bar-numbers">
                                        <span id="numMedical">20萬 / 30萬</span>
                                        <span class="gap-diff" id="diffMedical">缺10萬</span>
                                    </div>
                                </div>
                            </div>

                            <div class="gap-bar-item">
                                <div class="gap-bar-header">
                                    <span class="gap-label">重大疾病</span>
                                    <span class="gap-percent" id="percentCritical" style="font-weight: bold; color: #667eea;">100%</span>
                                    <span class="gap-status" id="statusCritical">✅ 足夠</span>
                                </div>
                                <div class="gap-bar-visual">
                                    <div class="gap-bar-bg">
                                        <div class="gap-bar-fill gap-bar-ok" id="barCritical" style="width: 100%"></div>
                                        <div class="gap-bar-target"></div>
                                    </div>
                                    <div class="gap-bar-numbers">
                                        <span id="numCritical">100萬 / 100萬</span>
                                        <span class="gap-diff gap-ok" id="diffCritical">達標</span>
                                    </div>
                                </div>
                            </div>

                            <div class="gap-bar-item">
                                <div class="gap-bar-header">
                                    <span class="gap-label">癌症保障</span>
                                    <span class="gap-percent" id="percentCancer" style="font-weight: bold; color: #667eea;">60%</span>
                                    <span class="gap-status" id="statusCancer">⚠️ 不足</span>
                                </div>
                                <div class="gap-bar-visual">
                                    <div class="gap-bar-bg">
                                        <div class="gap-bar-fill" id="barCancer" style="width: 50%"></div>
                                        <div class="gap-bar-target"></div>
                                    </div>
                                    <div class="gap-bar-numbers">
                                        <span id="numCancer">50萬 / 100萬</span>
                                        <span class="gap-diff" id="diffCancer">缺50萬</span>
                                    </div>
                                </div>
                            </div>

                            <div class="gap-bar-item">
                                <div class="gap-bar-header">
                                    <span class="gap-label">長照保障</span>
                                    <span class="gap-percent" id="percentLTC" style="font-weight: bold; color: #667eea;">0%</span>
                                    <span class="gap-status" id="statusLTC">❌ 嚴重不足</span>
                                </div>
                                <div class="gap-bar-visual">
                                    <div class="gap-bar-bg">
                                        <div class="gap-bar-fill gap-bar-danger" id="barLTC" style="width: 0%"></div>
                                        <div class="gap-bar-target"></div>
                                    </div>
                                    <div class="gap-bar-numbers">
                                        <span id="numLTC">0萬 / 4.5萬/月</span>
                                        <span class="gap-diff gap-danger" id="diffLTC">缺4.5萬/月</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- 財務衝擊試算 -->
                    <div class="financial-impact-box">
                        <h4>💰 財務衝擊試算（以癌症為例）</h4>
                        <div class="impact-calc">
                            <div class="impact-row">
                                <span class="impact-label">治療總費用：</span>
                                <span class="impact-value">100 萬元</span>
                            </div>
                            <div class="impact-row">
                                <span class="impact-label">健保給付：</span>
                                <span class="impact-value">-10 萬元</span>
                            </div>
                            <div class="impact-row">
                                <span class="impact-label">目前保單賠付：</span>
                                <span class="impact-value impact-insurance" id="impactInsurance">-44 萬元</span>
                            </div>
                            <div class="impact-row impact-total">
                                <span class="impact-label">您需要自費：</span>
                                <span class="impact-value impact-danger" id="impactSelfPay">46 萬元</span>
                            </div>
                        </div>
                        <p class="impact-note">⚠️ 這筆費用相當於您 <span id="impactMonths">4.8</span> 個月的家庭收入</p>
                    </div>
                </div>
            </section>
        </div>

        <!-- 第三頁：解決方案 -->
        <div id="page3" class="page">
            <section class="card">
                <h2 class="card-title">🛡️ 專屬解決方案與配置建議</h2>
                <div class="section-intro" id="solutionIntroText">
                    <!-- 動態顯示情感化引導文字 -->
                </div>
                
                <!-- 問題與解決方案對比區 -->
                <div class="problem-solution-grid" id="problemSolutionGrid" style="margin-bottom: 30px;">
                    <!-- 動態生成問題與解決方案對比 -->
                </div>

                <!-- 缺口優先級分類 -->
                <div class="priority-classification">
                    <h3 class="section-subtitle">🎯 缺口優先級排序</h3>
                    
                    <div class="priority-grid">
                        <!-- 高危缺口 -->
                        <div class="priority-box priority-critical">
                            <div class="priority-header">
                                <span class="priority-icon">🔴</span>
                                <h4>高危缺口（必須立即處理）</h4>
                            </div>
                            <ul class="priority-list" id="criticalGaps">
                                <li>壽險保障不足 300萬（現 300萬 / 建議 600萬）</li>
                                <li>長照保障完全缺乏（建議 4.5萬/月）</li>
                            </ul>
                        </div>

                        <!-- 次要缺口 -->
                        <div class="priority-box priority-medium">
                            <div class="priority-header">
                                <span class="priority-icon">🟡</span>
                                <h4>次要缺口（建議補強）</h4>
                            </div>
                            <ul class="priority-list" id="mediumGaps">
                                <li>實支實付不足 10萬（現 20萬 / 建議 30萬）</li>
                                <li>癌症保障不足 50萬（現 50萬 / 建議 100萬）</li>
                            </ul>
                        </div>

                        <!-- 優化項目 -->
                        <div class="priority-box priority-low">
                            <div class="priority-header">
                                <span class="priority-icon">🟢</span>
                                <h4>優化項目（錦上添花）</h4>
                            </div>
                            <ul class="priority-list" id="lowGaps">
                                <li>意外保障已達標 ✅</li>
                                <li>重大疾病已達標 ✅</li>
                                <li>可考慮增加儲蓄型保單</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <!-- 三種配置方案 -->
                <div class="solution-plans">
                    <h3 class="section-subtitle">💼 三種分級配置方案</h3>
                    
                    <div class="plans-comparison">
                        <!-- 方案 A -->
                        <div class="plan-card plan-basic">
                            <div class="plan-badge">A 方案</div>
                            <h4 class="plan-title">基礎防護</h4>
                            <div class="plan-price">
                                <span class="price-amount" id="planAPrice">6-8</span>
                                <span class="price-unit">萬/年</span>
                            </div>
                            <div class="plan-desc">優先處理高危缺口，適合預算有限的客戶</div>
                            
                            <div class="plan-coverage">
                                <h5>包含項目：</h5>
                                <ul class="plan-list" id="planAItems">
                                    <li><span class="check">✔️</span> 增加壽險 300萬</li>
                                    <li><span class="check">✔️</span> 基礎長照防護 2萬/月</li>
                                    <li><span class="check">✔️</span> 維持現有意外、醫療保障</li>
                                </ul>
                            </div>
                            
                            <div class="plan-result">
                                <strong>補強後總分：</strong>
                                <span class="result-score" id="planAScore">75</span>
                                <span class="result-label">（待改善 → 良好）</span>
                            </div>
                            
                            <label class="plan-checkbox">
                                <input type="checkbox" id="selectPlanA"> 選擇此方案
                            </label>
                        </div>

                        <!-- 方案 B -->
                        <div class="plan-card plan-complete">
                            <div class="plan-badge plan-badge-recommended">B 方案 ⭐ 推薦</div>
                            <h4 class="plan-title">完整保障</h4>
                            <div class="plan-price">
                                <span class="price-amount" id="planBPrice">12-15</span>
                                <span class="price-unit">萬/年</span>
                            </div>
                            <div class="plan-desc">補足所有高危+次要缺口，全面防護</div>
                            
                            <div class="plan-coverage">
                                <h5>包含項目：</h5>
                                <ul class="plan-list" id="planBItems">
                                    <li><span class="check">✔️</span> A 方案所有內容</li>
                                    <li><span class="check">✔️</span> 提升實支實付至 30萬</li>
                                    <li><span class="check">✔️</span> 增加癌症一次金 50萬</li>
                                    <li><span class="check">✔️</span> 長照提升至 4.5萬/月</li>
                                </ul>
                            </div>
                            
                            <div class="plan-result">
                                <strong>補強後總分：</strong>
                                <span class="result-score" id="planBScore">92</span>
                                <span class="result-label result-excellent">（待改善 → 優秀）</span>
                            </div>
                            
                            <label class="plan-checkbox">
                                <input type="checkbox" id="selectPlanB" checked> 選擇此方案
                            </label>
                        </div>

                        <!-- 方案 C -->
                        <div class="plan-card plan-premium">
                            <div class="plan-badge">C 方案</div>
                            <h4 class="plan-title">頂級規劃</h4>
                            <div class="plan-price">
                                <span class="price-amount" id="planCPrice">20-25</span>
                                <span class="price-unit">萬/年</span>
                            </div>
                            <div class="plan-desc">全險種覆蓋+儲蓄，適合高收入家庭</div>
                            
                            <div class="plan-coverage">
                                <h5>包含項目：</h5>
                                <ul class="plan-list" id="planCItems">
                                    <li><span class="check">✔️</span> B 方案所有內容</li>
                                    <li><span class="check">✔️</span> 增額終身壽險 200萬</li>
                                    <li><span class="check">✔️</span> 高額失能月領 3萬/月</li>
                                    <li><span class="check">✔️</span> 還本型儲蓄保單</li>
                                </ul>
                            </div>
                            
                            <div class="plan-result">
                                <strong>補強後總分：</strong>
                                <span class="result-score" id="planCScore">98</span>
                                <span class="result-label result-excellent">（待改善 → 頂級）</span>
                            </div>
                            
                            <label class="plan-checkbox">
                                <input type="checkbox" id="selectPlanC"> 選擇此方案
                            </label>
                        </div>
                    </div>
                </div>

                <!-- 保費負擔能力檢測 -->
                <div class="affordability-check">
                    <h4>📊 保費負擔能力檢測</h4>
                    <div class="affordability-grid">
                        <div class="affordability-item">
                            <span class="afford-label">家庭年收入：</span>
                            <span class="afford-value" id="affordIncome">96萬</span>
                        </div>
                        <div class="affordability-item">
                            <span class="afford-label">B 方案年保費：</span>
                            <span class="afford-value" id="affordPremium">13.5萬</span>
                        </div>
                        <div class="affordability-item">
                            <span class="afford-label">佔收入比例：</span>
                            <span class="afford-value" id="affordRatio">14.1%</span>
                        </div>
                        <div class="affordability-item">
                            <span class="afford-label">評估：</span>
                            <span class="afford-status" id="affordStatus">✅ 合理範圍（10-15%）</span>
                        </div>
                    </div>
                    <p class="afford-note">⚠️ 建議保費佔家庭收入比例不超過 15%，以免影響生活品質</p>
                </div>
            </section>
        </div>

        <!-- 第四頁：實際醫療開銷 vs 保單賠付 -->
        <div id="page4" class="page">
            <section class="card">
                <h2 class="card-title">🎭 情境模擬</h2>
                
                <!-- 智能推薦提示 -->
                <div id="scenarioRecommendation" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; padding: 20px; border-radius: 12px; margin-bottom: 25px; box-shadow: 0 4px 15px rgba(240, 147, 251, 0.3);">
                    <div style="display: flex; align-items: center; gap: 15px;">
                        <div style="font-size: 2.5rem;">🎯</div>
                        <div style="flex: 1;">
                            <div style="font-size: 1.1rem; font-weight: 600; margin-bottom: 8px;">根據您的年齡和風險評估，以下 3 個情境最值得關注：</div>
                            <div id="recommendedScenarios" style="font-size: 0.95rem; opacity: 0.95;">
                                ⚡ 癌症治療  •  💉 CAR-T免疫療法  •  🦠 器官移植
                            </div>
                        </div>
                    </div>
                </div>

                <div class="tab-container">
                    <div class="tab-buttons">
                        <button class="tab-button active" data-tab="cancer">癌症治療</button>
                        <button class="tab-button" data-tab="pelvis">骨盆粉碎性骨折</button>
                        <button class="tab-button" data-tab="stroke">急性腦中風</button>
                        <button class="tab-button" data-tab="heart">冠狀動脈繞道手術</button>
                        <button class="tab-button" data-tab="cart">CAR-T免疫療法</button>
                        <button class="tab-button" data-tab="proton">質子治療</button>
                        <button class="tab-button" data-tab="icu">ICU重症照護</button>
                        <button class="tab-button" data-tab="transplant">器官移植</button>
                        <button class="tab-button" data-tab="longcare">長照照顧</button>
                    </div>

                    <!-- 癌症治療標籤頁 -->
                    <div class="tab-content active" id="cancer-tab">
                        <p style="text-align: center; margin-bottom: 20px;">癌症三期新式治療總費用 100 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="cancerCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="cancerPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">100萬</div>
                                <p>標靶/基因治療</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">10萬</div>
                                <p>部分項目給付</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="cancerPayout">44萬</div>
                                <p>實支 <span id="cancerMedicalPayout">20</span> 萬 + 癌症 <span id="cancerCancerPayout">24</span> 萬 + 重大 <span id="cancerCriticalPayout">0</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="cancerSelfPay">46萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- 骨盆粉碎性骨折標籤頁 -->
                    <div class="tab-content" id="pelvis-tab">
                        <p style="text-align: center; margin-bottom: 20px;">骨盆粉碎性骨折重建手術總費用 80 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="pelvisCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="pelvisPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">80萬</div>
                                <p>重建手術 + 復健</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">15萬</div>
                                <p>基本手術費用</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="pelvisPayout">36萬</div>
                                <p>實支 <span id="pelvisMedicalPayout">20</span> 萬 + 手術 <span id="pelvisSurgeryPayout">16</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="pelvisSelfPay">29萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- 急性腦中風標籤頁 -->
                    <div class="tab-content" id="stroke-tab">
                        <p style="text-align: center; margin-bottom: 20px;">急性腦中風先進治療總費用 120 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="strokeCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="strokePieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">120萬</div>
                                <p>取栓手術 + 復健</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">20萬</div>
                                <p>部分項目給付</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="strokePayout">50萬</div>
                                <p>實支 <span id="strokeMedicalPayout">20</span> 萬 + 重大疾病 <span id="strokeCriticalPayout">30</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="strokeSelfPay">50萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- 冠狀動脈繞道手術標籤頁 -->
                    <div class="tab-content" id="heart-tab">
                        <p style="text-align: center; margin-bottom: 20px;">冠狀動脈繞道手術總費用 90 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="heartCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="heartPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">90萬</div>
                                <p>達文西手術 + 住院</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">12萬</div>
                                <p>傳統手術給付</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="heartPayout">36萬</div>
                                <p>實支 <span id="heartMedicalPayout">20</span> 萬 + 手術 <span id="heartSurgeryPayout">16</span> 萬 + 重大 <span id="heartCriticalPayout">0</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="heartSelfPay">42萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- CAR-T 免疫療法標籤頁 -->
                    <div class="tab-content" id="cart-tab">
                        <p style="text-align: center; margin-bottom: 20px;">CAR-T 免疫療法（血癌）總費用 300 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="cartCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="cartPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">300萬</div>
                                <p>個人化免疫細胞療法</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">0萬</div>
                                <p>目前未納入健保</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="cartPayout">70萬</div>
                                <p>實支 <span id="cartMedicalPayout">20</span> 萬 + 癌症 <span id="cartCancerPayout">50</span> 萬 + 重大 <span id="cartCriticalPayout">0</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="cartSelfPay">230萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- 質子治療標籤頁 -->
                    <div class="tab-content" id="proton-tab">
                        <p style="text-align: center; margin-bottom: 20px;">質子治療（實體腫瘤）總費用 200 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="protonCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="protonPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">200萬</div>
                                <p>精準質子放射療法</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">5萬</div>
                                <p>僅給付部分項目</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="protonPayout">70萬</div>
                                <p>實支 <span id="protonMedicalPayout">20</span> 萬 + 癌症 <span id="protonCancerPayout">30</span> 萬 + 重大 <span id="protonCriticalPayout">0</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="protonSelfPay">125萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- ICU 重症照護標籤頁 -->
                    <div class="tab-content" id="icu-tab">
                        <p style="text-align: center; margin-bottom: 20px;">ICU 重症照護 30 天總費用 150 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="icuCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="icuPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">150萬</div>
                                <p>ICU + 葉克膜 + 藥物</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">30萬</div>
                                <p>基本照護費用</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="icuPayout">50萬</div>
                                <p>實支 <span id="icuMedicalPayout">20</span> 萬 + 重疾 <span id="icuCriticalPayout">30</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="icuSelfPay">70萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- 器官移植標籤頁 -->
                    <div class="tab-content" id="transplant-tab">
                        <p style="text-align: center; margin-bottom: 20px;">器官移植（肝/腎）總費用 250 萬元分析</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="transplantCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">自費佔比</h4>
                                <canvas id="transplantPieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總治療費用</h3>
                                <div class="comparison-value">250萬</div>
                                <p>手術 + 術後照護 + 抗排斥藥</p>
                            </div>
                            <div class="comparison-item">
                                <h3>健保給付</h3>
                                <div class="comparison-value">50萬</div>
                                <p>基本手術費用</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單賠付</h3>
                                <div class="comparison-value" id="transplantPayout">56萬</div>
                                <p>實支 <span id="transplantMedicalPayout">20</span> 萬 + 重大 <span id="transplantCriticalPayout">50</span> 萬</p>
                            </div>
                            <div class="comparison-item">
                                <h3>自付金額</h3>
                                <div class="comparison-value coverage-bad" id="transplantSelfPay">144萬</div>
                                <p>需額外準備</p>
                            </div>
                        </div>
                    </div>

                    <!-- 長照照顧標籤頁 -->
                    <div class="tab-content" id="longcare-tab">
                        <p style="text-align: center; margin-bottom: 20px;">長期照護 10 年總開銷 540 萬元分析（假設每月 4.5 萬）</p>

                        <div class="chart-grid">
                            <div class="chart-container">
                                <canvas id="longcareCostChart"></canvas>
                            </div>
                            <div class="chart-container">
                                <h4 style="text-align: center; margin-bottom: 10px;">月支出佔比</h4>
                                <canvas id="longcarePieChart"></canvas>
                            </div>
                        </div>

                        <div class="comparison-grid">
                            <div class="comparison-item">
                                <h3>總照護費用（10年）</h3>
                                <div class="comparison-value">540萬</div>
                                <p>看護 + 醫療耗材 + 復健</p>
                            </div>
                            <div class="comparison-item">
                                <h3>政府補助</h3>
                                <div class="comparison-value">36萬</div>
                                <p>長照2.0 補助（每月約3千）</p>
                            </div>
                            <div class="comparison-item">
                                <h3>保單給付（10年）</h3>
                                <div class="comparison-value" id="longcarePayout">0萬</div>
                                <p>長照險月領 <span id="longcareMonthly">0</span> 萬 × 120月</p>
                            </div>
                            <div class="comparison-item">
                                <h3>家庭自付（10年）</h3>
                                <div class="comparison-value coverage-bad" id="longcareSelfPay">504萬</div>
                                <p>每月需自籌 <span id="longcareMonthlyGap">4.2</span> 萬</p>
                            </div>
                        </div>

                        <div style="background: #fff3cd; padding: 20px; border-radius: 10px; margin-top: 20px;">
                            <h4 style="color: #856404; margin-bottom: 15px;">💡 長照財務衝擊說明</h4>
                            <ul style="color: #856404; line-height: 1.8;">
                                <li>• <strong>平均照護時長：</strong>失能者平均需要長期照護 7-10 年</li>
                                <li>• <strong>每月開銷明細：</strong>外籍看護 2.5萬 + 醫療耗材 0.8萬 + 復健 0.5萬 + 其他 0.7萬</li>
                                <li>• <strong>家庭負擔：</strong>若無長照險，每月 4.5 萬相當於一般家庭 50-60% 的收入</li>
                                <li>• <strong>建議配置：</strong>長照險月給付至少 4.5 萬，搭配失能險月領 3 萬以上</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </section>
        </div>

        <!-- 第五頁：未來醫療趨勢與費用預估 -->
        <div id="page5" class="page">
            <section class="card">
                <h2 class="card-title">🔮 未來醫療趨勢與長期保障規劃</h2>
                <div class="section-intro">
                    健保負擔逐年下降，新式治療自費比例攀升，提前規劃才能安心面對未來
                </div>

                <!-- 健保給付趨勢 -->
                <div class="nhi-trend-section">
                    <h3 class="section-subtitle">📉 台灣健保給付趨勢（過去與未來）</h3>
                    <div class="chart-container">
                        <canvas id="nhiTrendChart"></canvas>
                    </div>
                    <div class="trend-highlights">
                        <div class="trend-card trend-warning">
                            <div class="trend-icon">⚠️</div>
                            <h4>健保給付比例下降</h4>
                            <p>過去10年從 85% 降至 72%，未來預計持續下降至 60%</p>
                        </div>
                        <div class="trend-card trend-danger">
                            <div class="trend-icon">💰</div>
                            <h4>自費項目增加</h4>
                            <p>標靶藥物、免疫療法、精準醫療等新技術多數需自費</p>
                        </div>
                        <div class="trend-card trend-info">
                            <div class="trend-icon">🏥</div>
                            <h4>醫療費用通膨</h4>
                            <p>醫療費用年增率約 5-8%，遠高於一般物價通膨</p>
                        </div>
                    </div>
                </div>

                <!-- 新式治療對比表 -->
                <div class="treatment-comparison-section">
                    <h3 class="section-subtitle">🧬 新式治療費用對比表</h3>
                    <div class="treatment-table-wrapper">
                        <table class="treatment-table">
                            <thead>
                                <tr>
                                    <th>治療項目</th>
                                    <th>目前費用</th>
                                    <th>2030年預估</th>
                                    <th>健保給付</th>
                                    <th>自費比例</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td><strong>基因編輯治療</strong><br><small>CRISPR等技術</small></td>
                                    <td>—</td>
                                    <td class="cost-high">100-300萬</td>
                                    <td><span class="status-no">❌ 不給付</span></td>
                                    <td class="ratio-high">100%</td>
                                </tr>
                                <tr>
                                    <td><strong>CAR-T免疫療法</strong><br><small>血癌治療</small></td>
                                    <td class="cost-high">300-500萬</td>
                                    <td class="cost-high">250-400萬</td>
                                    <td><span class="status-no">❌ 不給付</span></td>
                                    <td class="ratio-high">100%</td>
                                </tr>
                                <tr>
                                    <td><strong>質子治療</strong><br><small>實體腫瘤</small></td>
                                    <td class="cost-high">150-250萬</td>
                                    <td class="cost-high">120-200萬</td>
                                    <td><span class="status-partial">⚠️ 部分給付</span></td>
                                    <td class="ratio-high">95%</td>
                                </tr>
                                <tr>
                                    <td><strong>AI精準手術</strong><br><small>機器人輔助</small></td>
                                    <td class="cost-medium">50-150萬</td>
                                    <td class="cost-medium">40-120萬</td>
                                    <td><span class="status-partial">⚠️ 部分給付</span></td>
                                    <td class="ratio-medium">80%</td>
                                </tr>
                                <tr>
                                    <td><strong>標靶藥物</strong><br><small>進階癌症治療</small></td>
                                    <td class="cost-medium">30-100萬</td>
                                    <td class="cost-high">50-200萬</td>
                                    <td><span class="status-partial">⚠️ 部分給付</span></td>
                                    <td class="ratio-medium">70%</td>
                                </tr>
                                <tr>
                                    <td><strong>器官3D列印</strong><br><small>客製化移植</small></td>
                                    <td>—</td>
                                    <td class="cost-high">100-300萬</td>
                                    <td><span class="status-no">❌ 不給付</span></td>
                                    <td class="ratio-high">100%</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

                <!-- 分階段保障規劃 -->
                <div class="timeline-planning-section">
                    <h3 class="section-subtitle">📅 10/20/30年分階段保障規劃</h3>
                    <div class="timeline-wrapper">
                        <div class="timeline-item timeline-phase1">
                            <div class="timeline-badge">第1-5年</div>
                            <div class="timeline-content">
                                <h4>🎯 優先補強高危缺口</h4>
                                <ul>
                                    <li>壽險、意外險達標準值</li>
                                    <li>實支實付提升至 30萬</li>
                                    <li>重大疾病、癌症險建立基礎防護</li>
                                </ul>
                                <div class="timeline-budget">預估年保費：<strong>8-12萬</strong></div>
                            </div>
                        </div>

                        <div class="timeline-item timeline-phase2">
                            <div class="timeline-badge">第6-15年</div>
                            <div class="timeline-content">
                                <h4>🛡️ 完整醫療+重疾防護</h4>
                                <ul>
                                    <li>雙實支實付（應對高額醫療）</li>
                                    <li>癌症險提升至100萬以上</li>
                                    <li>開始規劃失能、長照保障</li>
                                    <li>考慮增額終身壽險（儲蓄+保障）</li>
                                </ul>
                                <div class="timeline-budget">預估年保費：<strong>15-20萬</strong></div>
                            </div>
                        </div>

                        <div class="timeline-item timeline-phase3">
                            <div class="timeline-badge">第16-30年</div>
                            <div class="timeline-content">
                                <h4>💼 長照+退休現金流</h4>
                                <ul>
                                    <li>長照險月給付 4.5萬以上</li>
                                    <li>退休年金保險（穩定現金流）</li>
                                    <li>醫療險轉為終身型</li>
                                    <li>資產傳承規劃（增額壽險）</li>
                                </ul>
                                <div class="timeline-budget">預估年保費：<strong>20-30萬</strong></div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- 通膨對照計算器 -->
                <div class="inflation-calculator">
                    <h3 class="section-subtitle">💡 醫療費用通膨對照</h3>
                    <div class="inflation-controls">
                        <label>
                            醫療費用年增率：
                            <input type="range" id="inflationRate" min="3" max="10" value="6" step="0.5">
                            <span id="inflationValue">6%</span>
                        </label>
                        <label>
                            預測年數：
                            <input type="range" id="inflationYears" min="5" max="30" value="20" step="5">
                            <span id="yearsValue">20年</span>
                        </label>
                    </div>
                    <div class="inflation-result">
                        <div class="inflation-card">
                            <h4>今天的50萬實支實付</h4>
                            <div class="inflation-arrow">⬇️</div>
                            <h4><span id="futureValue">20</span>年後購買力剩</h4>
                            <div class="inflation-value" id="inflationResult">15.6萬</div>
                            <p class="inflation-note">建議定期檢視並調整保額，以維持購買力</p>
                        </div>
                    </div>
                </div>

                <!-- 未來趨勢圖表 -->
                <div class="future-chart-section">
                    <h3 class="section-subtitle">📈 未來醫療費用成長預測</h3>
                    <div class="chart-container">
                        <canvas id="futureCostChart"></canvas>
                    </div>
                </div>
            </section>
        </div>
    </div>

    <script>
        // 依年齡給出理想建議（參考千頁2）
        function getIdealByAge(age) {
            age = Number(age) || 40;
            return {
                death: age < 50 ? 600 : 300,
                accidentalDeath: 600,
                reimbursement: 30,
                criticalIllness: 100,
                cancer: 100,
                surgery: 16,
                accidentalHospital: 3000,
                illnessHospital: 3000,
                longTermCare: 4.5 // 萬/月
            };
        }

        function updateIdealHints() {
            const age = parseInt(document.getElementById('clientAge')?.value || '40', 10);
            const ideal = getIdealByAge(age);
            const setIdeal = (key, val) => {
                const span = document.querySelector(`[data-ideal="${key}"]`);
                if (span) span.textContent = val;
            };
            setIdeal('death', ideal.death);
            setIdeal('accidentalDeath', ideal.accidentalDeath);
            setIdeal('reimbursement', ideal.reimbursement);
            setIdeal('criticalIllness', ideal.criticalIllness);
            setIdeal('cancer', ideal.cancer);
            setIdeal('surgery', ideal.surgery);
            setIdeal('accidentalHospital', ideal.accidentalHospital);
            setIdeal('illnessHospital', ideal.illnessHospital);
            setIdeal('longTermCare', ideal.longTermCare);
        }

        // 頁面切換功能
        function showPage(pageNumber) {
            // 隱藏所有頁面
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            
            // 移除所有導航按鈕的active類
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // 顯示選定的頁面
            document.getElementById('page' + pageNumber).classList.add('active');
            
            // 為選定的導航按鈕添加active類
            document.querySelectorAll('.nav-btn')[pageNumber - 1].classList.add('active');

            // 進入第4/5頁時初始化或更新圖表
            if (pageNumber === 4) {
                setupMedicalTabsOnce();
                initMedicalCostCharts();
            } else if (pageNumber === 5) {
                initFutureTrendChart();
            }
        }
        
        // 選項卡切換功能
        function showTab(tabName) {
            // 隱藏所有選項卡內容
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // 移除所有選項卡按鈕的active類
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // 顯示選定的選項卡內容
            document.getElementById('tab-' + tabName).classList.add('active');
            
            // 為選定的選項卡按鈕添加active類
            document.querySelectorAll('.tab-btn').forEach(btn => {
                if (btn.textContent.includes(tabName === 'young' ? '單身期' : tabName === 'family' ? '家庭期' : '退休期')) {
                    btn.classList.add('active');
                }
            });
        }
        
        // 風險問答切換功能
        function toggleAnswer(id) {
            const answer = document.getElementById('answer' + id);
            if (answer.style.display === 'block') {
                answer.style.display = 'none';
            } else {
                answer.style.display = 'block';
            }
        }

        // 生成分析報告
        let lastAnalysisData = null;

        function generateAnalysis() {
            // 獲取表單數據
            const clientName = document.getElementById('clientName').value;
            const clientAge = parseInt(document.getElementById('clientAge').value);
            // 年收入若未填，改以月收入 * 12 推算
            const annualIncomeInput = document.getElementById('annualIncome');
            const monthlyIncomeInput = document.getElementById('monthlyIncome');
            let annualIncome = parseFloat(annualIncomeInput?.value || '');
            if (!annualIncome || isNaN(annualIncome)) {
                const m = parseFloat(monthlyIncomeInput?.value || '0');
                annualIncome = Math.round(m * 12);
            }
            const deathBenefit = parseInt(document.getElementById('deathBenefit').value);
            const accidentDeath = parseInt(document.getElementById('accidentDeath').value);
            const medicalLimit = parseInt(document.getElementById('medicalLimit').value);
            const criticalIllness = parseInt(document.getElementById('criticalIllness').value);
            const cancerBenefit = parseInt(document.getElementById('cancerBenefit').value);
            const longTermCare = parseFloat(document.getElementById('longTermCare').value);
            const surgeryBenefit = parseInt(document.getElementById('surgeryBenefit')?.value || 16);
            const accidentalHospital = parseInt(document.getElementById('accidentalHospital')?.value || 0);
            const illnessHospital = parseInt(document.getElementById('illnessHospital')?.value || 0);
            const disability = parseFloat(document.getElementById('disability')?.value || 0); // 萬/月
            
            // 保存分析數據供其他頁面使用
            lastAnalysisData = {
                name: clientName,
                age: clientAge,
                annualIncome: annualIncome,
                deathBenefit: deathBenefit,
                accidentDeath: accidentDeath,
                medicalLimit: medicalLimit,
                criticalIllness: criticalIllness,
                cancerBenefit: cancerBenefit,
                longTermCare: longTermCare,
                surgeryBenefit: surgeryBenefit,
                accidentalHospital: accidentalHospital,
                illnessHospital: illnessHospital,
                disability: disability
            };
            
            // 判斷人生階段
            let lifeStage, lifeStageText;
            if (clientAge >= 20 && clientAge <= 35) {
                lifeStage = 'young';
                lifeStageText = '單身期';
            } else if (clientAge >= 36 && clientAge <= 50) {
                lifeStage = 'family';
                lifeStageText = '家庭期';
            } else {
                lifeStage = 'retirement';
                lifeStageText = '退休期';
            }
            
            // 計算總保障額度
            const totalCoverage = deathBenefit + accidentDeath + medicalLimit + 
                                 criticalIllness + cancerBenefit + (longTermCare * 12);
            
            // 顯示分析結果並跳轉到第二頁
            alert(`親愛的 ${clientName} 客戶：

您的保障分析已完成！

📊 總保障額度：約 ${Math.round(totalCoverage).toLocaleString()} 萬元
🎯 人生階段：${lifeStageText}
💰 年收入：${annualIncome} 萬元

即將為您顯示詳細的保障分析...`);
            
            // 跳轉到第二頁（新版頁面會自動初始化）
            showPage(2);
        }
        
        // 更新第二頁分析內容
        // 舊版函數已廢棄，保留空殼以防其他地方引用
        function updateStageAnalysis(lifeStage, data) {
            // 已由新版 initPage2Analysis 取代
            console.log('updateStageAnalysis 已廢棄，請使用 initPage2Analysis');
        }
        
        // 舊版函數已廢棄
        function updateSolutionContent(lifeStage, data) {
            // 已由新版 initPage3Solutions 取代
            console.log('updateSolutionContent 已廢棄，請使用 initPage3Solutions');
        }
        
        // 舊版函數已廢棄
        function evaluateCoverage(type, meetsStandard, standard) {
            // 已廢棄，僅保留以防其他地方引用
            if (meetsStandard) {
                return `<span class="checkmark">✅</span> ${type} (符合標準: ${standard})`;
            } else {
                return `<span class="crossmark">❌</span> ${type} (建議提升至: ${standard})`;
            }
        }

        // ===== 以下為第4/5頁圖表與互動（取自 ds4 概念，調整為本頁欄位）=====
        let cancerChart, pelvisChart, strokeChart, heartChart, futureChart;
        let tabsBound = false;

        function getFormDataForMedical() {
            const read = id => {
                const el = document.getElementById(id);
                return el && el.value !== '' ? parseFloat(el.value) || 0 : 0;
            };
            return {
                medicalLimit: read('medicalLimit'),
                cancerBenefit: read('cancerBenefit'),
                criticalIllness: read('criticalIllness'),
                // 優先讀取手術保額欄位，fallback 16 萬
                surgeryBenefit: (function(){
                    const v = read('surgeryBenefit');
                    return v && !isNaN(v) ? v : 16;
                })()
            };
        }

        function updateMedicalCaseDOM(fd) {
            const setTxt = (id, v) => { const el = document.getElementById(id); if (el) el.textContent = v; };
            
            // 癌症
            const cancerMedicalPay = Math.min(fd.medicalLimit, 100 - 10);
            const cancerCancerPay = Math.min(fd.cancerBenefit, 24);
            const cancerCriticalPay = fd.criticalIllness;
            const cancerPayout = cancerMedicalPay + cancerCancerPay + cancerCriticalPay;
            const cancerSelf = Math.max(0, 100 - 10 - cancerPayout);
            setTxt('cancerPayout', `${Math.round(cancerPayout)}萬`);
            setTxt('cancerMedicalPayout', Math.round(cancerMedicalPay));
            setTxt('cancerCancerPayout', Math.round(cancerCancerPay));
            setTxt('cancerCriticalPayout', Math.round(cancerCriticalPay));
            setTxt('cancerSelfPay', `${Math.round(cancerSelf)}萬`);

            // 骨盆
            const pelvisMedicalPay = Math.min(fd.medicalLimit, 80 - 15);
            const pelvisPayout = pelvisMedicalPay + Math.min(fd.surgeryBenefit, 16);
            const pelvisSelf = Math.max(0, 80 - 15 - pelvisPayout);
            setTxt('pelvisPayout', `${Math.round(pelvisPayout)}萬`);
            setTxt('pelvisMedicalPayout', Math.round(pelvisMedicalPay));
            setTxt('pelvisSurgeryPayout', Math.min(fd.surgeryBenefit, 16));
            setTxt('pelvisSelfPay', `${Math.round(pelvisSelf)}萬`);

            // 中風
            const strokeMedicalPay = Math.min(fd.medicalLimit, 120 - 20);
            const strokeCriticalPay = fd.criticalIllness;
            const strokePayout = strokeMedicalPay + strokeCriticalPay;
            const strokeSelf = Math.max(0, 120 - 20 - strokePayout);
            setTxt('strokePayout', `${Math.round(strokePayout)}萬`);
            setTxt('strokeMedicalPayout', Math.round(strokeMedicalPay));
            setTxt('strokeCriticalPayout', Math.round(strokeCriticalPay));
            setTxt('strokeSelfPay', `${Math.round(strokeSelf)}萬`);

            // 心臟
            const heartMedicalPay = Math.min(fd.medicalLimit, 90 - 12);
            const heartSurgeryPay = Math.min(fd.surgeryBenefit, 16);
            const heartCriticalPay = fd.criticalIllness;
            const heartPayout = heartMedicalPay + heartSurgeryPay + heartCriticalPay;
            const heartSelf = Math.max(0, 90 - 12 - heartPayout);
            setTxt('heartPayout', `${Math.round(heartPayout)}萬`);
            setTxt('heartMedicalPayout', Math.round(heartMedicalPay));
            setTxt('heartSurgeryPayout', Math.round(heartSurgeryPay));
            setTxt('heartCriticalPayout', Math.round(heartCriticalPay));
            setTxt('heartSelfPay', `${Math.round(heartSelf)}萬`);
            
            // CAR-T免疫療法
            const cartMedicalPay = Math.min(fd.medicalLimit, 300 - 20);
            const cartCancerPay = Math.min(fd.cancerBenefit, 50);
            const cartCriticalPay = fd.criticalIllness;
            const cartPayout = cartMedicalPay + cartCancerPay + cartCriticalPay;
            const cartSelf = Math.max(0, 300 - 20 - cartPayout);
            setTxt('cartPayout', `${Math.round(cartPayout)}萬`);
            setTxt('cartMedicalPayout', Math.round(cartMedicalPay));
            setTxt('cartCancerPayout', Math.round(cartCancerPay));
            setTxt('cartCriticalPayout', Math.round(cartCriticalPay));
            setTxt('cartSelfPay', `${Math.round(cartSelf)}萬`);
            
            // 質子治療
            const protonMedicalPay = Math.min(fd.medicalLimit, 150 - 10);
            const protonCancerPay = Math.min(fd.cancerBenefit, 30);
            const protonCriticalPay = fd.criticalIllness;
            const protonPayout = protonMedicalPay + protonCancerPay + protonCriticalPay;
            const protonSelf = Math.max(0, 150 - 10 - protonPayout);
            setTxt('protonPayout', `${Math.round(protonPayout)}萬`);
            setTxt('protonMedicalPayout', Math.round(protonMedicalPay));
            setTxt('protonCancerPayout', Math.round(protonCancerPay));
            setTxt('protonCriticalPayout', Math.round(protonCriticalPay));
            setTxt('protonSelfPay', `${Math.round(protonSelf)}萬`);
            
            // ICU重症照護
            const icuMedicalPay = Math.min(fd.medicalLimit, 200 - 25);
            const icuCriticalPay = fd.criticalIllness;
            const icuPayout = icuMedicalPay + icuCriticalPay;
            const icuSelf = Math.max(0, 200 - 25 - icuPayout);
            setTxt('icuPayout', `${Math.round(icuPayout)}萬`);
            setTxt('icuMedicalPayout', Math.round(icuMedicalPay));
            setTxt('icuCriticalPayout', Math.round(icuCriticalPay));
            setTxt('icuSelfPay', `${Math.round(icuSelf)}萬`);
            
            // 器官移植
            const transplantMedicalPay = Math.min(fd.medicalLimit, 250 - 30);
            const transplantCriticalPay = fd.criticalIllness;
            const transplantPayout = transplantMedicalPay + transplantCriticalPay;
            const transplantSelf = Math.max(0, 250 - 30 - transplantPayout);
            setTxt('transplantPayout', `${Math.round(transplantPayout)}萬`);
            setTxt('transplantMedicalPayout', Math.round(transplantMedicalPay));
            setTxt('transplantCriticalPayout', Math.round(transplantCriticalPay));
            setTxt('transplantSelfPay', `${Math.round(transplantSelf)}萬`);
            
            // 長照照顧
            const longcarePayout = (fd.medicalLimit > 0 ? 10 : 0) + Math.min((lastAnalysisData?.longTermCare || 0) * 120, 540);
            const longcareSelf = Math.max(0, 540 - 36 - longcarePayout);
            setTxt('longcarePayout', `${Math.round(longcarePayout)}萬`);
            setTxt('longcareSelfPay', `${Math.round(longcareSelf)}萬`);
        }

        function initMedicalCostCharts() {
            const fd = getFormDataForMedical();
            updateMedicalCaseDOM(fd);

            // 銷毀舊圖表
            try { if (cancerChart) cancerChart.destroy(); } catch(e){}
            try { if (pelvisChart) pelvisChart.destroy(); } catch(e){}
            try { if (strokeChart) strokeChart.destroy(); } catch(e){}
            try { if (heartChart) heartChart.destroy(); } catch(e){}

            const barOptions = {
                responsive: true,
                maintainAspectRatio: false,
                scales: { y: { beginAtZero: true, title: { display: true, text: '金額 (萬元)' } } },
                plugins: { legend: { display: false }, tooltip: { callbacks: { label: ctx => `${ctx.parsed.y} 萬元` } } }
            };

            // 癌症
            const cancerCtx = document.getElementById('cancerCostChart');
            if (cancerCtx) {
                const payout = Math.min(fd.medicalLimit, 100 - 10) + Math.min(fd.cancerBenefit, 24) + fd.criticalIllness;
                const selfPay = Math.max(0, 100 - 10 - payout);
                cancerChart = new Chart(cancerCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [100, 10, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // 骨盆
            const pelvisCtx = document.getElementById('pelvisCostChart');
            if (pelvisCtx) {
                const payout = Math.min(fd.medicalLimit, 80 - 15) + Math.min(fd.surgeryBenefit, 16);
                const selfPay = Math.max(0, 80 - 15 - payout);
                pelvisChart = new Chart(pelvisCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [80, 15, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // 中風
            const strokeCtx = document.getElementById('strokeCostChart');
            if (strokeCtx) {
                const payout = Math.min(fd.medicalLimit, 120 - 20) + fd.criticalIllness;
                const selfPay = Math.max(0, 120 - 20 - payout);
                strokeChart = new Chart(strokeCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [120, 20, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // 心臟
            const heartCtx = document.getElementById('heartCostChart');
            if (heartCtx) {
                const payout = Math.min(fd.medicalLimit, 90 - 12) + Math.min(fd.surgeryBenefit, 16) + fd.criticalIllness;
                const selfPay = Math.max(0, 90 - 12 - payout);
                heartChart = new Chart(heartCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [90, 12, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // CAR-T 免疫療法
            const cartCtx = document.getElementById('cartCostChart');
            if (cartCtx) {
                const payout = Math.min(fd.medicalLimit, 300 - 20) + Math.min(fd.cancerBenefit, 50) + fd.criticalIllness;
                const selfPay = Math.max(0, 300 - 20 - payout);
                try { const existing = Chart.getChart(cartCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(cartCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [300, 20, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // 質子治療
            const protonCtx = document.getElementById('protonCostChart');
            if (protonCtx) {
                const payout = Math.min(fd.medicalLimit, 150 - 10) + Math.min(fd.cancerBenefit, 30) + fd.criticalIllness;
                const selfPay = Math.max(0, 150 - 10 - payout);
                try { const existing = Chart.getChart(protonCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(protonCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [150, 10, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // ICU重症照護
            const icuCtx = document.getElementById('icuCostChart');
            if (icuCtx) {
                const payout = Math.min(fd.medicalLimit, 200 - 25) + fd.criticalIllness;
                const selfPay = Math.max(0, 200 - 25 - payout);
                try { const existing = Chart.getChart(icuCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(icuCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [200, 25, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // 器官移植
            const transplantCtx = document.getElementById('transplantCostChart');
            if (transplantCtx) {
                const payout = Math.min(fd.medicalLimit, 250 - 30) + fd.criticalIllness;
                const selfPay = Math.max(0, 250 - 30 - payout);
                try { const existing = Chart.getChart(transplantCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(transplantCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總治療費用', '健保給付', '保單賠付', '自付金額'], datasets: [{
                        label: '金額(萬元)',
                        data: [250, 30, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // 長照照顧
            const longcareCtx = document.getElementById('longcareCostChart');
            if (longcareCtx) {
                const payout = (fd.medicalLimit > 0 ? 10 : 0) + Math.min((lastAnalysisData?.longTermCare || 0) * 120, 540); // 10年長照
                const selfPay = Math.max(0, 540 - 36 - payout);
                try { const existing = Chart.getChart(longcareCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(longcareCtx.getContext('2d'), {
                    type: 'bar',
                    data: { labels: ['總照護費用', '政府補助', '保單給付', '家庭自付'], datasets: [{
                        label: '金額(萬元)',
                        data: [540, 36, Math.round(payout), Math.round(selfPay)],
                        backgroundColor: ['rgba(52,152,219,0.7)','rgba(46,204,113,0.7)','rgba(155,89,182,0.7)','rgba(231,76,60,0.7)'],
                        borderColor: ['#3498db','#2ecc71','#9b59b6','#e74c3c'], borderWidth: 1
                    }]}, options: barOptions
                });
            }

            // ============ 圓餅圖初始化 ============
            const pieOptions = {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { position: 'right', labels: { font: { size: 11 }, padding: 10 } },
                    tooltip: {
                        callbacks: {
                            label: function(context) {
                                const label = context.label || '';
                                const value = context.parsed || 0;
                                const total = context.dataset.data.reduce((a, b) => a + b, 0);
                                const percent = total > 0 ? ((value / total) * 100).toFixed(1) : 0;
                                return `${label}: ${value}萬 (${percent}%)`;
                            }
                        }
                    }
                }
            };

            // 癌症圓餅圖
            const cancerPieCtx = document.getElementById('cancerPieChart');
            if (cancerPieCtx) {
                const payout = Math.min(fd.medicalLimit, 100 - 10) + Math.min(fd.cancerBenefit, 24) + fd.criticalIllness;
                const selfPay = Math.max(0, 100 - 10 - payout);
                try { const existing = Chart.getChart(cancerPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(cancerPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [18, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // 骨盆骨折圓餅圖
            const pelvisPieCtx = document.getElementById('pelvisPieChart');
            if (pelvisPieCtx) {
                const payout = Math.min(fd.medicalLimit, 80 - 15) + Math.min(fd.surgeryBenefit, 16);
                const selfPay = Math.max(0, 80 - 15 - payout);
                try { const existing = Chart.getChart(pelvisPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(pelvisPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [15, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // 中風圓餅圖
            const strokePieCtx = document.getElementById('strokePieChart');
            if (strokePieCtx) {
                const payout = Math.min(fd.medicalLimit, 120 - 20) + fd.criticalIllness;
                const selfPay = Math.max(0, 120 - 20 - payout);
                try { const existing = Chart.getChart(strokePieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(strokePieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [20, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // 心臟圓餅圖
            const heartPieCtx = document.getElementById('heartPieChart');
            if (heartPieCtx) {
                const payout = Math.min(fd.medicalLimit, 90 - 12) + Math.min(fd.surgeryBenefit, 16) + fd.criticalIllness;
                const selfPay = Math.max(0, 90 - 12 - payout);
                try { const existing = Chart.getChart(heartPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(heartPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [12, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // CAR-T圓餅圖
            const cartPieCtx = document.getElementById('cartPieChart');
            if (cartPieCtx) {
                const payout = Math.min(fd.medicalLimit, 300 - 20) + Math.min(fd.cancerBenefit, 50) + fd.criticalIllness;
                const selfPay = Math.max(0, 300 - 20 - payout);
                try { const existing = Chart.getChart(cartPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(cartPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [20, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // 質子治療圓餅圖
            const protonPieCtx = document.getElementById('protonPieChart');
            if (protonPieCtx) {
                const payout = Math.min(fd.medicalLimit, 150 - 10) + Math.min(fd.cancerBenefit, 30) + fd.criticalIllness;
                const selfPay = Math.max(0, 150 - 10 - payout);
                try { const existing = Chart.getChart(protonPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(protonPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [10, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // ICU圓餅圖
            const icuPieCtx = document.getElementById('icuPieChart');
            if (icuPieCtx) {
                const payout = Math.min(fd.medicalLimit, 200 - 25) + fd.criticalIllness;
                const selfPay = Math.max(0, 200 - 25 - payout);
                try { const existing = Chart.getChart(icuPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(icuPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [25, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // 器官移植圓餅圖
            const transplantPieCtx = document.getElementById('transplantPieChart');
            if (transplantPieCtx) {
                const payout = Math.min(fd.medicalLimit, 250 - 30) + fd.criticalIllness;
                const selfPay = Math.max(0, 250 - 30 - payout);
                try { const existing = Chart.getChart(transplantPieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(transplantPieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['健保給付', '保單賠付', '自付金額'],
                        datasets: [{
                            data: [30, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }

            // 長照圓餅圖
            const longcarePieCtx = document.getElementById('longcarePieChart');
            if (longcarePieCtx) {
                const payout = (fd.medicalLimit > 0 ? 10 : 0) + Math.min((lastAnalysisData?.longTermCare || 0) * 120, 540);
                const selfPay = Math.max(0, 540 - 36 - payout);
                try { const existing = Chart.getChart(longcarePieCtx); if (existing) existing.destroy(); } catch(e){}
                new Chart(longcarePieCtx.getContext('2d'), {
                    type: 'pie',
                    data: {
                        labels: ['政府補助', '保單給付', '家庭自付'],
                        datasets: [{
                            data: [36, Math.round(payout), Math.round(selfPay)],
                            backgroundColor: ['rgba(46,204,113,0.8)','rgba(155,89,182,0.8)','rgba(231,76,60,0.8)'],
                            borderColor: ['#2ecc71','#9b59b6','#e74c3c'],
                            borderWidth: 2
                        }]
                    },
                    options: pieOptions
                });
            }
        }

        // 🆕 智能情境推薦（根據年齡自動高亮相關情境）
        function updateScenarioRecommendation() {
            if (!lastAnalysisData) return;
            const age = lastAnalysisData.age || 40;
            
            let recommended = [];
            let recommendText = '';
            
            if (age < 36) {
                recommended = ['cancer', 'pelvis', 'heart'];
                recommendText = '⚡ 癌症治療  •  🦴 骨盆骨折  •  ❤️ 心血管手術';
            } else if (age < 51) {
                recommended = ['cancer', 'cart', 'stroke'];
                recommendText = '⚡ 癌症治療  •  💉 CAR-T免疫療法  •  🧠 急性腦中風';
            } else {
                recommended = ['longcare', 'transplant', 'icu'];
                recommendText = '👴 長照照顧  •  🦠 器官移植  •  🏥 ICU重症';
            }
            
            // 更新推薦文字
            const recEl = document.getElementById('recommendedScenarios');
            if (recEl) recEl.innerHTML = recommendText;
            
            // 高亮推薦的tab按鈕
            document.querySelectorAll('#page4 .tab-button').forEach(btn => {
                const tab = btn.getAttribute('data-tab');
                if (recommended.includes(tab)) {
                    btn.style.background = 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)';
                    btn.style.color = 'white';
                    btn.style.fontWeight = 'bold';
                    btn.style.boxShadow = '0 4px 15px rgba(240, 147, 251, 0.4)';
                } else {
                    btn.style.background = '';
                    btn.style.color = '';
                    btn.style.fontWeight = '';
                    btn.style.boxShadow = '';
                }
            });
        }

        function setupMedicalTabsOnce() {
            if (tabsBound) return;
            tabsBound = true;
            const container = document.querySelector('#page4 .tab-buttons');
            if (!container) return;
            container.addEventListener('click', (e) => {
                const btn = e.target.closest('.tab-button');
                if (!btn) return;
                const tab = btn.getAttribute('data-tab');
                document.querySelectorAll('#page4 .tab-button').forEach(b=>b.classList.remove('active'));
                btn.classList.add('active');
                document.querySelectorAll('#page4 .tab-content').forEach(c=>c.classList.remove('active'));
                const el = document.getElementById(`${tab}-tab`);
                if (el) el.classList.add('active');
            });
        }

        function initFutureTrendChart() {
            try { if (futureChart) futureChart.destroy(); } catch(e){}
            const ctxEl = document.getElementById('futureTrendChart');
            if (!ctxEl) return;
            const fd = getFormDataForMedical();
            futureChart = new Chart(ctxEl.getContext('2d'), {
                type: 'line',
                data: {
                    labels: ['2025', '2028', '2030', '2032', '2035'],
                    datasets: [
                        { label: '先進醫療平均費用', data: [30,45,60,80,120], borderColor: '#e74c3c', backgroundColor: 'rgba(231,76,60,0.1)', fill: true, tension: 0.4 },
                        { label: '目前實支實付額度', data: [fd.medicalLimit,fd.medicalLimit,fd.medicalLimit,fd.medicalLimit,fd.medicalLimit], borderColor: '#3498db', backgroundColor: 'rgba(52,152,219,0.1)', borderDash: [5,5], fill: true, tension: 0 }
                    ]
                },
                options: { responsive: true, maintainAspectRatio: false, scales: { y: { beginAtZero: true, title: { display: true, text: '金額 (萬元)' } } } }
            });
        }

        // 🆕 即時更新：當使用者修改第一頁參數時，即時更新所有頁面
        document.addEventListener('input', (e) => {
            const id = (e.target || {}).id || '';
            
            // 所有保險相關欄位
            const insuranceFields = [
                'deathBenefit', 'accidentDeath', 'medicalLimit', 
                'criticalIllness', 'cancerBenefit', 'longTermCare',
                'surgeryBenefit', 'accidentalHospital', 'illnessHospital', 'disability'
            ];
            
            // 基本資料欄位
            const basicFields = ['clientAge', 'monthlyIncome', 'annualIncome'];
            
            // 如果是保險欄位變動
            if (insuranceFields.includes(id)) {
                // 更新 lastAnalysisData
                if (lastAnalysisData) {
                    const value = parseFloat(document.getElementById(id).value) || 0;
                    if (id === 'deathBenefit') lastAnalysisData.deathBenefit = value;
                    else if (id === 'accidentDeath') lastAnalysisData.accidentDeath = value;
                    else if (id === 'medicalLimit') lastAnalysisData.medicalLimit = value;
                    else if (id === 'criticalIllness') lastAnalysisData.criticalIllness = value;
                    else if (id === 'cancerBenefit') lastAnalysisData.cancerBenefit = value;
                    else if (id === 'longTermCare') lastAnalysisData.longTermCare = value;
                    else if (id === 'surgeryBenefit') lastAnalysisData.surgeryBenefit = value;
                    else if (id === 'accidentalHospital') lastAnalysisData.accidentalHospital = value;
                    else if (id === 'illnessHospital') lastAnalysisData.illnessHospital = value;
                    else if (id === 'disability') lastAnalysisData.disability = value;
                    
                    // 即時更新當前頁面
                    const currentPage = document.querySelector('.page.active');
                    if (currentPage) {
                        const pageId = currentPage.id;
                        if (pageId === 'page2') {
                            const ideal = getIdealByAge(lastAnalysisData.age || 40);
                            updateQuickDiagnosis(ideal);
                            updateGapAnalysis(ideal);
                            updateGaugeChart();
                            updateFinancialImpact();
                        } else if (pageId === 'page3') {
                            initPage3Solutions();
                        } else if (pageId === 'page4') {
                            initMedicalCostCharts();
                        } else if (pageId === 'page5') {
                            initFutureTrendChart();
                        }
                    }
                }
            }
            
            // 如果是年齡變動
            if (id === 'clientAge') {
                updateIdealHints();
                if (lastAnalysisData) {
                    const age = parseInt(document.getElementById('clientAge').value) || 40;
                    lastAnalysisData.age = age;
                    
                    // 更新當前頁面
                    const currentPage = document.querySelector('.page.active');
                    if (currentPage) {
                        const pageId = currentPage.id;
                        if (pageId === 'page2') {
                            initPage2Analysis();
                        } else if (pageId === 'page3') {
                            initPage3Solutions();
                        } else if (pageId === 'page4') {
                            updateScenarioRecommendation();
                        }
                    }
                }
            }
            
            // 如果是收入變動
            if (id === 'monthlyIncome' || id === 'annualIncome') {
                if (lastAnalysisData) {
                    const monthly = parseFloat(document.getElementById('monthlyIncome')?.value || 0);
                    const annual = parseFloat(document.getElementById('annualIncome')?.value || 0);
                    lastAnalysisData.annualIncome = annual || (monthly * 12);
                    
                    // 更新第2頁的財務衝擊試算
                    if (document.getElementById('page2')?.classList.contains('active')) {
                        updateFinancialImpact();
                    }
                }
            }
        });

        // 初始化理想建議提示
        updateIdealHints();

        // ===== 第二頁：風險雷達圖與缺口分析 =====
        let riskRadarChart, gaugeChart;
        let lastGapAnalysis = null;

        function initPage2Analysis() {
            if (!lastAnalysisData) return;
            
            const age = lastAnalysisData.age || 40;
            const ideal = getIdealByAge(age);
            
            // 🆕 更新快速診斷卡
            updateQuickDiagnosis(ideal);
            
            // 更新情感引導文字
            updateEmotionalIntro(age);
            
            // 更新風險意識喚醒區
            updateRiskAwareness(age);
            
            // 更新風險雷達圖
            updateRiskRadar(age);
            
            // 更新真實數據卡片
            updateRiskStats(age);
            
            // 更新情境模擬
            updateScenarioCards();
            
            // 更新缺口分析
            updateGapAnalysis(ideal);
            
            // 更新儀表盤
            updateGaugeChart();
            
            // 更新財務衝擊試算
            updateFinancialImpact();
        }

        // 🆕 快速診斷卡更新
        function updateQuickDiagnosis(ideal) {
            const data = lastAnalysisData;
            if (!data) return;
            
            // 計算缾口詳情
            const gaps = [
                { label: '壽險', actual: data.deathBenefit, ideal: ideal.death },
                { label: '意外', actual: data.accidentDeath, ideal: ideal.accidentalDeath },
                { label: '實支', actual: data.medicalLimit, ideal: ideal.reimbursement },
                { label: '重疾', actual: data.criticalIllness, ideal: ideal.criticalIllness },
                { label: '癌症', actual: data.cancerBenefit, ideal: ideal.cancer },
                { label: '長照', actual: data.longTermCare, ideal: ideal.longTermCare }
            ];
            
            // 計算風險評分（0-100）
            const scores = gaps.map(gap => Math.min(100, (gap.actual / gap.ideal) * 100));
            const avgScore = Math.round(scores.reduce((a,b) => a+b, 0) / scores.length);
            
            // 找最大缾口
            let maxGap = gaps[0];
            let maxDiff = 0;
            gaps.forEach(gap => {
                const diff = gap.ideal - gap.actual;
                if (diff > maxDiff) {
                    maxDiff = diff;
                    maxGap = gap;
                }
            });
            const maxGapPercent = Math.round((maxGap.actual / maxGap.ideal) * 100);
            
            // 統計缾口數量
            const gapCount = gaps.filter(gap => (gap.actual / gap.ideal) < 0.9).length;
            const p0Count = gaps.filter(gap => (gap.actual / gap.ideal) < 0.5).length;
            const p1Count = gaps.filter(gap => {
                const ratio = gap.actual / gap.ideal;
                return ratio >= 0.5 && ratio < 0.9;
            }).length;
            
            // 更新顯示
            document.getElementById('quickRiskScore').textContent = avgScore;
            const levelEl = document.getElementById('quickRiskLevel');
            if (avgScore >= 80) {
                levelEl.textContent = '低風險';
                levelEl.style.color = '#a5d6a7';
            } else if (avgScore >= 60) {
                levelEl.textContent = '中高風險';
                levelEl.style.color = '#fff59d';
            } else {
                levelEl.textContent = '高風險';
                levelEl.style.color = '#ef9a9a';
            }
            
            document.getElementById('quickMaxGap').textContent = `${maxGap.label}險 ${Math.round(maxDiff)}萬`;
            document.getElementById('quickGapCount').textContent = gapCount;
            document.getElementById('quickPriority').textContent = `P0: ${p0Count}項`;
            
            // 智能建議
            const criticalGaps = gaps.filter(gap => (gap.actual / gap.ideal) < 0.5)
                .sort((a, b) => (b.ideal - b.actual) - (a.ideal - a.actual))
                .slice(0, 2);
            
            let recommendation = '';
            if (criticalGaps.length === 0) {
                recommendation = '您的保障规划整体良好，建議每年定期檢視即可';
            } else if (criticalGaps.length === 1) {
                recommendation = `優先處理 ${criticalGaps[0].label}險不足（缺 ${Math.round(criticalGaps[0].ideal - criticalGaps[0].actual)}萬），可大幅降低風險`;
            } else {
                recommendation = `優先處理 ${criticalGaps[0].label}險和${criticalGaps[1].label}險不足，可降低 80% 風險`;
            }
            document.getElementById('quickRecommendation').textContent = recommendation;
        }

        function updateEmotionalIntro(age) {
            const introEl = document.getElementById('emotionalIntro');
            if (!introEl) return;
            
            let introText = '';
            if (age < 36) {
                introText = '💭 <strong>您正處於人生最精彩的打拼期</strong>，充滿夢想與機會。但您是否想過：<span style="color: #e74c3c;">如果意外發生，您的夢想計劃可能被迫中斷？</span> 讓我們用數據幫您看清真實的風險...';
            } else if (age < 51) {
                introText = '💭 <strong>您正處於家庭責任最重的時期</strong>，作為家人的依靠。您是否擔心：<span style="color: #e74c3c;">如果有一天您倒下了，家人的生活會怎樣？</span> 以下數據將幫您評估真實的保障缺口...';
            } else {
                introText = '💭 <strong>您辛苦工作了一輩子</strong>，即將迎來退休生活。但您是否憂慮：<span style="color: #e74c3c;">退休金真的夠用嗎？晚年生活品質能維持嗎？</span> 讓我們一起檢視您的保障規劃...';
            }
            introEl.innerHTML = introText;
        }

        function updateRiskAwareness(age) {
            const awareEl = document.getElementById('riskAwareness');
            if (!awareEl) return;
            
            let awareHTML = '';
            if (age < 36) {
                awareHTML = `
                    <div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); color: white; padding: 25px; border-radius: 12px; margin-bottom: 20px;">
                        <h4 style="margin-bottom: 15px; font-size: 1.2rem;">🎯 單身期，您正面臨的現實挑戰：</h4>
                        <ul style="list-style: none; padding-left: 0; line-height: 1.8;">
                            <li style="margin-bottom: 10px;">💸 <strong>想像一下：</strong>一場意外可能讓您辛苦累積的積蓄瞬間歸零，夢想被迫延後...</li>
                            <li style="margin-bottom: 10px;">📊 <strong>每個月的房租、學貸壓力</strong>，讓您不敢輕易請假，深怕收入中斷</li>
                            <li style="margin-bottom: 10px;">🏥 <strong>醫療費用</strong>可能成為您前進路上的絆腳石，耗盡辛苦累積的積蓄</li>
                            <li>💍 <strong>結婚、買房的夢想</strong>很美，但沒有足夠的保障，這些計劃可能隨時破滅</li>
                        </ul>
                    </div>
                `;
            } else if (age < 51) {
                awareHTML = `
                    <div style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); color: white; padding: 25px; border-radius: 12px; margin-bottom: 20px;">
                        <h4 style="margin-bottom: 15px; font-size: 1.2rem;">👨‍👩‍👧‍👦 家庭期，您最擔心的家庭風險：</h4>
                        <ul style="list-style: none; padding-left: 0; line-height: 1.8;">
                            <li style="margin-bottom: 10px;">💔 <strong>作為家庭的頂梁柱</strong>，您是否想過：如果有一天您倒下了，家人的生活怎麼辦？</li>
                            <li style="margin-bottom: 10px;">💰 <strong>孩子的教育費用、房貸車貸</strong>，這些固定支出讓您不敢有任何閃失</li>
                            <li style="margin-bottom: 10px;">🎗️ <strong>癌症、重大疾病</strong>不再是遙遠的名詞，而是可能發生在身邊的真實威脅</li>
                            <li>🏥 <strong>您希望給家人最好的醫療品質</strong>，但高昂的費用可能成為沉重的負擔</li>
                        </ul>
                    </div>
                `;
            } else {
                awareHTML = `
                    <div style="background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); color: #2c3e50; padding: 25px; border-radius: 12px; margin-bottom: 20px;">
                        <h4 style="margin-bottom: 15px; font-size: 1.2rem;">🏖️ 退休期，您最關心的晚年議題：</h4>
                        <ul style="list-style: none; padding-left: 0; line-height: 1.8;">
                            <li style="margin-bottom: 10px;">💸 <strong>您辛苦工作了一輩子</strong>，是否擔心退休金不夠用，晚年生活品質下降？</li>
                            <li style="margin-bottom: 10px;">🏥 <strong>醫療看護費用</strong>越來越貴，一場大病可能耗盡您畢生的積蓄</li>
                            <li style="margin-bottom: 10px;">🦽 <strong>慢性病、失能風險增加</strong>，您是否擔心成為子女的負擔？</li>
                            <li>👨‍👩‍👧 <strong>您想為子女留下些什麼</strong>，但稅務規劃讓您感到困擾</li>
                        </ul>
                    </div>
                `;
            }
            awareEl.innerHTML = awareHTML;
        }

        function updateRiskRadar(age) {
            const ctx = document.getElementById('riskRadarChart');
            if (!ctx) return;
            
            // 根據年齡段計算風險分數
            let riskData;
            if (age < 36) {
                riskData = [30, 40, 25, 60, 20, 35]; // 年輕期：意外風險較高
            } else if (age < 51) {
                riskData = [60, 70, 55, 45, 40, 65]; // 中年期：癌症、心血管風險高
            } else {
                riskData = [75, 80, 70, 30, 85, 90]; // 老年期：重症、長照風險高
            }
            
            if (riskRadarChart) riskRadarChart.destroy();
            
            riskRadarChart = new Chart(ctx.getContext('2d'), {
                type: 'radar',
                data: {
                    labels: ['癌症', '心血管', '中風', '意外', '失能', '高額醫療'],
                    datasets: [{
                        label: '風險指數',
                        data: riskData,
                        backgroundColor: 'rgba(231, 76, 60, 0.2)',
                        borderColor: '#e74c3c',
                        borderWidth: 2,
                        pointBackgroundColor: '#e74c3c',
                        pointBorderColor: '#fff',
                        pointHoverBackgroundColor: '#fff',
                        pointHoverBorderColor: '#e74c3c'
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: true,
                    aspectRatio: 1,
                    scales: {
                        r: {
                            beginAtZero: true,
                            max: 100,
                            ticks: { stepSize: 20 }
                        }
                    },
                    plugins: {
                        legend: {
                            display: true,
                            position: 'top'
                        }
                    }
                }
            });
        }

        function updateRiskStats(age) {
            let criticalRate, avgCost, careYears;
            if (age < 36) {
                criticalRate = '3%'; avgCost = '25萬'; careYears = '5.2年';
            } else if (age < 51) {
                criticalRate = '8%'; avgCost = '45萬'; careYears = '7.3年';
            } else {
                criticalRate = '15%'; avgCost = '65萬'; careYears = '9.8年';
            }
            
            const setTxt = (id, txt) => { const el = document.getElementById(id); if (el) el.textContent = txt; };
            setTxt('criticalRate', criticalRate);
            setTxt('avgSelfPay', avgCost);
            setTxt('careYears', careYears);
        }

        function updateScenarioCards() {
            if (!lastAnalysisData) return;
            const data = getFormDataForMedical();
            
            // 癌症情境
            const cancerPayout = Math.min(data.medicalLimit, 100 - 10) + Math.min(data.cancerBenefit, 24) + data.criticalIllness;
            const cancerSelf = Math.max(0, 100 - 10 - cancerPayout);
            document.getElementById('scenarioCancerImpact').textContent = `自費缺口：${Math.round(cancerSelf)}萬`;
            
            // 意外情境
            const monthlyIncome = parseFloat(document.getElementById('monthlyIncome')?.value || 8);
            const disability = parseFloat(document.getElementById('disability')?.value || 0);
            const monthlyCare = 3; // 照護費用假設3萬/月
            const monthlyLoss = monthlyIncome + monthlyCare;
            const monthlyGap = Math.max(0, monthlyLoss - disability);
            document.getElementById('scenarioAccidentCost').textContent = `${monthlyLoss.toFixed(1)}萬`;
            document.getElementById('scenarioAccidentImpact').textContent = `月缺口：${monthlyGap.toFixed(1)}萬`;
            
            // 重症情境（ICU）
            const icuPayout = Math.min(data.medicalLimit, 200 - 25) + data.criticalIllness;
            const icuSelf = Math.max(0, 200 - 25 - icuPayout);
            document.getElementById('scenarioCriticalImpact').textContent = `自費缺口：${Math.round(icuSelf)}萬`;
        }

        function updateGapAnalysis(ideal) {
            const data = lastAnalysisData;
            if (!data) return;
            
            const gaps = [
                { label: '壽險保障', actual: data.deathBenefit, ideal: ideal.death, id: 'Death' },
                { label: '意外保障', actual: data.accidentDeath, ideal: ideal.accidentalDeath, id: 'Accident' },
                { label: '實支實付', actual: data.medicalLimit, ideal: ideal.reimbursement, id: 'Medical' },
                { label: '重大疾病', actual: data.criticalIllness, ideal: ideal.criticalIllness, id: 'Critical' },
                { label: '癌症保障', actual: data.cancerBenefit, ideal: ideal.cancer, id: 'Cancer' },
                { label: '長照保障', actual: data.longTermCare, ideal: ideal.longTermCare, id: 'LTC', isMonthly: true }
            ];
            
            lastGapAnalysis = gaps;
            
            gaps.forEach(gap => {
                const percent = Math.min(100, (gap.actual / gap.ideal) * 100);
                const diff = gap.ideal - gap.actual;
                const isOk = percent >= 90;
                const isDanger = percent < 50;
                
                // 🆕 更新達成率百分比
                const percentEl = document.getElementById(`percent${gap.id}`);
                if (percentEl) {
                    percentEl.textContent = `${Math.round(percent)}%`;
                    if (isOk) percentEl.style.color = '#2ecc71';
                    else if (isDanger) percentEl.style.color = '#e74c3c';
                    else percentEl.style.color = '#f39c12';
                }
                
                // 更新進度條
                const barEl = document.getElementById(`bar${gap.id}`);
                if (barEl) {
                    barEl.style.width = `${percent}%`;
                    barEl.className = 'gap-bar-fill';
                    if (isOk) barEl.classList.add('gap-bar-ok');
                    else if (isDanger) barEl.classList.add('gap-bar-danger');
                }
                
                // 更新數字
                const numEl = document.getElementById(`num${gap.id}`);
                if (numEl) {
                    const unit = gap.isMonthly ? '萬/月' : '萬';
                    numEl.textContent = `${gap.actual}${unit} / ${gap.ideal}${unit}`;
                }
                
                // 更新差距
                const diffEl = document.getElementById(`diff${gap.id}`);
                if (diffEl) {
                    if (isOk) {
                        diffEl.textContent = '達標';
                        diffEl.className = 'gap-diff gap-ok';
                    } else {
                        const unit = gap.isMonthly ? '萬/月' : '萬';
                        diffEl.textContent = `缺${diff.toFixed(1)}${unit}`;
                        diffEl.className = isDanger ? 'gap-diff gap-danger' : 'gap-diff';
                    }
                }
                
                // 更新狀態
                const statusEl = document.getElementById(`status${gap.id}`);
                if (statusEl) {
                    if (isOk) statusEl.textContent = '✅ 足夠';
                    else if (isDanger) statusEl.textContent = '❌ 嚴重不足';
                    else statusEl.textContent = '⚠️ 不足';
                }
            });
        }

        function updateGaugeChart() {
            if (!lastGapAnalysis) return;
            
            // 計算總分（0-100）
            const scores = lastGapAnalysis.map(gap => {
                const percent = Math.min(100, (gap.actual / gap.ideal) * 100);
                return percent;
            });
            const totalScore = Math.round(scores.reduce((a,b) => a+b, 0) / scores.length);
            
            const scoreEl = document.getElementById('totalScore');
            const ratingEl = document.getElementById('scoreRating');
            if (scoreEl) scoreEl.textContent = totalScore;
            if (ratingEl) {
                if (totalScore >= 81) ratingEl.textContent = '優秀';
                else if (totalScore >= 61) ratingEl.textContent = '需要改善';
                else ratingEl.textContent = '高風險';
            }
            
            // 繪製儀表盤（簡易版，使用Canvas手繪）
            const canvas = document.getElementById('gaugeChart');
            if (!canvas) return;
            const ctx = canvas.getContext('2d');
            const centerX = canvas.width / 2;
            const centerY = canvas.height / 2 + 20;
            const radius = 100;
            
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            // 繪製背景弧
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, Math.PI, 2 * Math.PI);
            ctx.lineWidth = 20;
            ctx.strokeStyle = '#e1e8ed';
            ctx.stroke();
            
            // 繪製分數弧
            const angle = Math.PI + (totalScore / 100) * Math.PI;
            ctx.beginPath();
            ctx.arc(centerX, centerY, radius, Math.PI, angle);
            ctx.lineWidth = 20;
            if (totalScore >= 81) ctx.strokeStyle = '#2ecc71';
            else if (totalScore >= 61) ctx.strokeStyle = '#f39c12';
            else ctx.strokeStyle = '#e74c3c';
            ctx.stroke();
            
            // 繪製指針
            const pointerAngle = Math.PI + (totalScore / 100) * Math.PI;
            const pointerX = centerX + radius * 0.7 * Math.cos(pointerAngle);
            const pointerY = centerY + radius * 0.7 * Math.sin(pointerAngle);
            ctx.beginPath();
            ctx.moveTo(centerX, centerY);
            ctx.lineTo(pointerX, pointerY);
            ctx.lineWidth = 3;
            ctx.strokeStyle = '#2c3e50';
            ctx.stroke();
        }

        function updateFinancialImpact() {
            if (!lastAnalysisData) return;
            const data = getFormDataForMedical();
            const monthlyIncome = parseFloat(document.getElementById('monthlyIncome')?.value || 8);
            
            const totalCost = 100;
            const nhi = 10;
            const insurance = Math.min(data.medicalLimit, 100 - 10) + Math.min(data.cancerBenefit, 24) + data.criticalIllness;
            const selfPay = Math.max(0, totalCost - nhi - insurance);
            
            document.getElementById('impactInsurance').textContent = `-${Math.round(insurance)} 萬元`;
            document.getElementById('impactSelfPay').textContent = `${Math.round(selfPay)} 萬元`;
            
            const months = (selfPay / monthlyIncome).toFixed(1);
            document.getElementById('impactMonths').textContent = months;
        }

        // ===== 第三頁：優先級分類與方案規劃 =====
        function initPage3Solutions() {
            if (!lastGapAnalysis) return;
            
            // 更新情感化引導文字
            updateSolutionIntro(lastAnalysisData.age || 40);
            
            // 更新問題與解決方案對比
            updateProblemSolutionGrid(lastAnalysisData.age || 40);
            
            // 分類缺口
            const critical = [];
            const medium = [];
            const low = [];
            
            lastGapAnalysis.forEach(gap => {
                const percent = Math.min(100, (gap.actual / gap.ideal) * 100);
                const diff = gap.ideal - gap.actual;
                const unit = gap.isMonthly ? '萬/月' : '萬';
                const text = `${gap.label}不足 ${diff.toFixed(1)}${unit}（現 ${gap.actual}${unit} / 建議 ${gap.ideal}${unit}）`;
                
                if (percent < 50) critical.push(text);
                else if (percent < 90) medium.push(text);
                else low.push(`${gap.label}已達標 ✅`);
            });
            
            // 填充缺口列表
            const fillList = (id, items) => {
                const el = document.getElementById(id);
                if (!el) return;
                if (items.length === 0) {
                    el.innerHTML = '<li>目前無缺口 ✅</li>';
                } else {
                    el.innerHTML = items.map(item => `<li>${item}</li>`).join('');
                }
            };
            
            fillList('criticalGaps', critical);
            fillList('mediumGaps', medium);
            fillList('lowGaps', low.length > 0 ? low : ['可考慮增加儲蓄型保單']);
            
            // 更新保費負擔能力
            const annualIncome = lastAnalysisData?.annualIncome || 96;
            const planBPremium = 13.5; // 假設B方案年保費
            const ratio = ((planBPremium / annualIncome) * 100).toFixed(1);
            
            document.getElementById('affordIncome').textContent = `${annualIncome}萬`;
            document.getElementById('affordPremium').textContent = `${planBPremium}萬`;
            document.getElementById('affordRatio').textContent = `${ratio}%`;
            
            const affordStatus = document.getElementById('affordStatus');
            if (ratio <= 15) {
                affordStatus.textContent = '✅ 合理範圍（10-15%）';
                affordStatus.style.color = '#2ecc71';
            } else {
                affordStatus.textContent = '⚠️ 超出建議（>15%）';
                affordStatus.style.color = '#f39c12';
            }
        }

        function updateSolutionIntro(age) {
            const introEl = document.getElementById('solutionIntroText');
            if (!introEl) return;
            
            let introText = '';
            if (age < 36) {
                introText = '讓我們為您打造一個<strong style="color: #3498db;">安心追夢的保障計劃</strong>，讓您無後顧之憂地追求精彩人生：';
            } else if (age < 51) {
                introText = '讓我們為您的家庭建立一個<strong style="color: #e74c3c;">堅實的保護網</strong>，確保無論發生什麼，家人的生活都能繼續美好：';
            } else {
                introText = '讓我們為您的退休生活規劃一個<strong style="color: #f39c12;">安心的保障</strong>，讓您的晚年生活像您期待的那樣精彩：';
            }
            introEl.innerHTML = introText;
        }

        function updateProblemSolutionGrid(age) {
            const gridEl = document.getElementById('problemSolutionGrid');
            if (!gridEl) return;
            
            let gridHTML = '';
            if (age < 36) {
                gridHTML = `
                    <div class="problem-column">
                        <h3>🎯 單身期最讓您擔憂的現實</h3>
                        <ul class="risk-list">
                            <li>• 您正在為夢想打拼，但<strong style="color: #e74c3c;">一場意外</strong>可能讓所有努力付諸東流</li>
                            <li>• 每個月的固定支出像<strong>無形的壓力</strong>，讓您不敢有任何閃失</li>
                            <li>• <strong>醫療費用</strong>可能成為您前進路上的絆腳石，耗盡辛苦累積的積蓄</li>
                            <li>• 結婚、買房的夢想很美，但<strong>沒有足夠的保障</strong>，這些計劃可能隨時破滅</li>
                        </ul>
                    </div>
                    <div class="solution-column">
                        <h3>🛡️ 為您量身打造的安心方案</h3>
                        <ul class="solution-list">
                            <li>💪 <strong>夢想守護傘</strong>：600萬意外保障，讓您無懼意外風險，勇敢追夢</li>
                            <li>🏥 <strong>醫療安心網</strong>：30萬實支實付，讓您享受最好的醫療品質</li>
                            <li>❤️ <strong>健康守護金</strong>：100萬重大疾病一次金，生病時也能安心治療</li>
                            <li>🎯 <strong>愛的延續</strong>：200萬壽險保障，為您在乎的人留下愛的承諾</li>
                            <li>💰 <strong>未來儲備金</strong>：強制儲蓄計劃，為您的美好未來做準備</li>
                        </ul>
                    </div>
                `;
            } else if (age < 51) {
                gridHTML = `
                    <div class="problem-column">
                        <h3>👨‍👩‍👧‍👦 家庭期最讓您揪心的擔憂</h3>
                        <ul class="risk-list">
                            <li>• 作為家庭的頂梁柱，您是否<strong style="color: #e74c3c;">夜裡輾轉難眠</strong>，擔心家人的未來？</li>
                            <li>• <strong>孩子的教育費用、房貸車貸</strong>，這些重擔讓您不敢有任何意外</li>
                            <li>• 癌症、重大疾病不再是電視上的故事，而是<strong>可能發生在身邊的威脅</strong></li>
                            <li>• 您希望給家人最好的醫療照顧，但<strong>高昂的費用</strong>可能成為沉重負擔</li>
                            <li>• <strong>失能風險</strong>就像一把懸在頭上的劍，讓您時刻感到不安</li>
                        </ul>
                    </div>
                    <div class="solution-column">
                        <h3>🛡️ 為您家庭打造的堅實堡壘</h3>
                        <ul class="solution-list">
                            <li>👨‍👩‍👧‍👦 <strong>家庭守護神</strong>：500萬壽險保障，確保家人生活無憂的承諾</li>
                            <li>🎗️ <strong>健康雙重防護</strong>：癌症險+重大疾病險，雙重保障對抗疾病威脅</li>
                            <li>🦽 <strong>尊嚴生活保障</strong>：4.5萬月給付長照險，失能時也能維持生活品質</li>
                            <li>🎓 <strong>教育夢想基金</strong>：專款專用教育金，確保孩子教育不受影響</li>
                            <li>💎 <strong>智慧理財規劃</strong>：還本型保險，讓保障與儲蓄同步進行</li>
                        </ul>
                    </div>
                `;
            } else {
                gridHTML = `
                    <div class="problem-column">
                        <h3>🏖️ 退休期最讓您憂慮的未來</h3>
                        <ul class="risk-list">
                            <li>• 您辛苦工作了一輩子，是否擔心<strong style="color: #e74c3c;">退休金不夠用</strong>，晚年生活品質下降？</li>
                            <li>• <strong>醫療看護費用</strong>越來越貴，一場大病可能耗盡您畢生的積蓄</li>
                            <li>• 慢性病、失能風險增加，您是否擔心<strong>成為子女的負擔</strong>？</li>
                            <li>• 您想為子女留下些什麼，但<strong>複雜的稅務規劃</strong>讓您感到困擾</li>
                            <li>• <strong>通貨膨脹</strong>像無形的小偷，悄悄侵蝕您的退休金購買力</li>
                        </ul>
                    </div>
                    <div class="solution-column">
                        <h3>🛡️ 為您晚年打造的安心藍圖</h3>
                        <ul class="solution-list">
                            <li>🏖️ <strong>尊嚴晚年保障</strong>：4.5萬月給付長照險，讓您有尊嚴地享受晚年</li>
                            <li>💰 <strong>穩定現金流</strong>：退休年金保險，對抗長壽風險的智慧選擇</li>
                            <li>🏥 <strong>終身醫療守護</strong>：終身醫療保障，讓您無後顧之憂</li>
                            <li>❤️ <strong>愛的傳承規劃</strong>：增額壽險，為子女留下美好與祝福</li>
                            <li>📈 <strong>財富增值策略</strong>：類全委投資型保單，專業管理對抗通膨</li>
                        </ul>
                    </div>
                `;
            }
            gridEl.innerHTML = gridHTML;
        }

        // ===== 第四頁：增加圓餅圖 =====
        let pieCharts = {};

        function initMedicalPieCharts() {
            const data = getFormDataForMedical();
            
            // 定義每個案例的數據
            const scenarios = [
                { id: 'cancer', total: 100, nhi: 10, medical: Math.min(data.medicalLimit, 90), cancer: Math.min(data.cancerBenefit, 24), critical: data.criticalIllness },
                { id: 'pelvis', total: 80, nhi: 15, medical: Math.min(data.medicalLimit, 65), surgery: Math.min(data.surgeryBenefit, 16) },
                { id: 'stroke', total: 120, nhi: 20, medical: Math.min(data.medicalLimit, 100), critical: data.criticalIllness },
                { id: 'heart', total: 90, nhi: 12, medical: Math.min(data.medicalLimit, 78), surgery: Math.min(data.surgeryBenefit, 16), critical: data.criticalIllness },
                { id: 'cart', total: 300, nhi: 20, medical: Math.min(data.medicalLimit, 280), cancer: Math.min(data.cancerBenefit, 50), critical: data.criticalIllness },
                { id: 'proton', total: 150, nhi: 10, medical: Math.min(data.medicalLimit, 140), cancer: Math.min(data.cancerBenefit, 30), critical: data.criticalIllness },
                { id: 'icu', total: 200, nhi: 25, medical: Math.min(data.medicalLimit, 175), critical: data.criticalIllness },
                { id: 'transplant', total: 250, nhi: 30, medical: Math.min(data.medicalLimit, 220), critical: data.criticalIllness },
                { id: 'longcare', total: 540, nhi: 36, longcare: data.longTermCare * 120 }
            ];
            
            scenarios.forEach(sc => {
                const payout = (sc.medical || 0) + (sc.cancer || 0) + (sc.surgery || 0) + (sc.critical || 0) + (sc.longcare || 0);
                const selfPay = Math.max(0, sc.total - sc.nhi - payout);
                
                const canvasId = `${sc.id}PieChart`;
                const canvas = document.getElementById(canvasId);
                if (!canvas) return;
                
                if (pieCharts[sc.id]) pieCharts[sc.id].destroy();
                
                const selfPayPercent = ((selfPay / sc.total) * 100).toFixed(1);
                
                pieCharts[sc.id] = new Chart(canvas.getContext('2d'), {
                    type: 'doughnut',
                    data: {
                        labels: sc.id === 'longcare' ? ['政府補助', '保單', '自付'] : ['健保', '保單', '自費'],
                        datasets: [{
                            data: [sc.nhi, payout, selfPay],
                            backgroundColor: ['#2ecc71', '#3498db', '#e74c3c'],
                            borderWidth: 2,
                            borderColor: '#fff'
                        }]
                    },
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        plugins: {
                            legend: { position: 'bottom' },
                            tooltip: {
                                callbacks: {
                                    label: (ctx) => `${ctx.label}: ${ctx.parsed}萬 (${((ctx.parsed/sc.total)*100).toFixed(1)}%)`
                                }
                            }
                        }
                    }
                });
                
                // 更新DOM中的支付數據
                if (sc.id === 'longcare') {
                    const payoutEl = document.getElementById('longcarePayout');
                    const selfPayEl = document.getElementById('longcareSelfPay');
                    const monthlyEl = document.getElementById('longcareMonthly');
                    const monthlyGapEl = document.getElementById('longcareMonthlyGap');
                    if (payoutEl) payoutEl.textContent = `${Math.round(payout)}萬`;
                    if (selfPayEl) selfPayEl.textContent = `${Math.round(selfPay)}萬`;
                    if (monthlyEl) monthlyEl.textContent = data.longTermCare.toFixed(1);
                    if (monthlyGapEl) monthlyGapEl.textContent = ((selfPay / 120)).toFixed(1);
                } else {
                    const updatePayout = (prefix, medVal, othVal, othLabel) => {
                        const payoutEl = document.getElementById(`${prefix}Payout`);
                        const selfPayEl = document.getElementById(`${prefix}SelfPay`);
                        if (payoutEl) payoutEl.textContent = `${Math.round(payout)}萬`;
                        if (selfPayEl) selfPayEl.textContent = `${Math.round(selfPay)}萬`;
                    };
                    
                    if (sc.id === 'cancer' || sc.id === 'cart' || sc.id === 'proton') {
                        updatePayout(sc.id, sc.medical, sc.cancer, '癌症');
                    } else if (sc.id === 'pelvis' || sc.id === 'heart') {
                        updatePayout(sc.id, sc.medical, sc.surgery, '手術');
                    } else if (sc.id === 'stroke' || sc.id === 'icu') {
                        updatePayout(sc.id, sc.medical, sc.critical, '重疾');
                    } else if (sc.id === 'transplant') {
                        const payoutEl = document.getElementById('transplantPayout');
                        const selfPayEl = document.getElementById('transplantSelfPay');
                        if (payoutEl) payoutEl.textContent = `${Math.round(payout)}萬`;
                        if (selfPayEl) selfPayEl.textContent = `${Math.round(selfPay)}萬`;
                    }
                }
            });
        }

        // ===== 第五頁：健保趨勢圖與通膨計算器 =====
        let nhiTrendChart, futureCostChart;

        function initPage5Trends() {
            initNHITrendChart();
            initFutureCostChart();
            setupInflationCalculator();
        }

        function initNHITrendChart() {
            const canvas = document.getElementById('nhiTrendChart');
            if (!canvas) return;
            
            if (nhiTrendChart) nhiTrendChart.destroy();
            
            nhiTrendChart = new Chart(canvas.getContext('2d'), {
                type: 'line',
                data: {
                    labels: ['2015', '2018', '2021', '2025', '2028', '2031', '2035'],
                    datasets: [
                        {
                            label: '健保給付比例',
                            data: [85, 80, 75, 72, 68, 64, 60],
                            borderColor: '#e74c3c',
                            backgroundColor: 'rgba(231, 76, 60, 0.1)',
                            fill: true,
                            tension: 0.4
                        },
                        {
                            label: '自費比例',
                            data: [15, 20, 25, 28, 32, 36, 40],
                            borderColor: '#f39c12',
                            backgroundColor: 'rgba(243, 156, 18, 0.1)',
                            fill: true,
                            tension: 0.4
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            max: 100,
                            ticks: { callback: (val) => val + '%' }
                        }
                    }
                }
            });
        }

        function initFutureCostChart() {
            const canvas = document.getElementById('futureCostChart');
            if (!canvas) return;
            
            if (futureCostChart) futureCostChart.destroy();
            
            futureCostChart = new Chart(canvas.getContext('2d'), {
                type: 'line',
                data: {
                    labels: ['2025', '2028', '2030', '2032', '2035'],
                    datasets: [
                        {
                            label: '先進醫療平均費用',
                            data: [50, 75, 100, 135, 180],
                            borderColor: '#e74c3c',
                            backgroundColor: 'rgba(231, 76, 60, 0.1)',
                            fill: true,
                            tension: 0.4
                        },
                        {
                            label: '一般實支實付額度',
                            data: [30, 30, 30, 30, 30],
                            borderColor: '#3498db',
                            backgroundColor: 'rgba(52, 152, 219, 0.1)',
                            borderDash: [5, 5],
                            fill: false,
                            tension: 0
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: true,
                            title: { display: true, text: '金額（萬元）' }
                        }
                    }
                }
            });
        }

        function setupInflationCalculator() {
            const rateInput = document.getElementById('inflationRate');
            const yearsInput = document.getElementById('inflationYears');
            const rateValue = document.getElementById('inflationValue');
            const yearsValue = document.getElementById('yearsValue');
            const resultEl = document.getElementById('inflationResult');
            
            const calculate = () => {
                const rate = parseFloat(rateInput.value) / 100;
                const years = parseInt(yearsInput.value);
                const current = 50;
                const future = current / Math.pow(1 + rate, years);
                
                rateValue.textContent = `${(rate * 100).toFixed(1)}%`;
                yearsValue.textContent = `${years}年`;
                resultEl.textContent = `${future.toFixed(1)}萬`;
                document.getElementById('futureValue').textContent = years;
            };
            
            if (rateInput) rateInput.addEventListener('input', calculate);
            if (yearsInput) yearsInput.addEventListener('input', calculate);
            
            calculate();
        }

        // ===== 更新 showPage 以觸發各頁初始化 =====
        const originalShowPage = showPage;
        showPage = function(pageNumber) {
            originalShowPage(pageNumber);
            
            if (pageNumber === 2) {
                setTimeout(initPage2Analysis, 100);
            } else if (pageNumber === 3) {
                setTimeout(initPage3Solutions, 100);
            } else if (pageNumber === 4) {
                setupMedicalTabsOnce();
                setTimeout(() => {
                    initMedicalCostCharts();
                    initMedicalPieCharts();
                }, 100);
            } else if (pageNumber === 5) {
                setTimeout(initPage5Trends, 100);
            }
        };

        // PDF建議書下載功能
        function downloadProposal() {
            if (!lastAnalysisData) {
                alert('請先生成分析報告！');
                return;
            }

            // 使用瀏覽器原生列印功能
            const originalDisplay = [];
            const pages = document.querySelectorAll('.page');
            
            // 隱藏第1頁和第5頁，只顯示第2、4、3頁
            pages.forEach((page, index) => {
                originalDisplay[index] = page.style.display;
                const pageNum = index + 1;
                if (pageNum === 2 || pageNum === 3 || pageNum === 4) {
                    page.style.display = 'block';
                } else {
                    page.style.display = 'none';
                }
            });

            // 只印重點內容，避免超長與被截斷
            const restoreDisplayMap = new Map();
            const rememberAndSet = (el, prop, value) => {
                if (!el) return;
                const key = `${prop}::${restoreDisplayMap.size}`;
                restoreDisplayMap.set(el, el.style[prop]);
                el.style[prop] = value;
            };
            const hideSelector = (selector) => {
                document.querySelectorAll(selector).forEach(el => rememberAndSet(el, 'display', 'none'));
            };

            // 第2頁：保留快速診斷與缺口儀表板，隱藏重內容避免切頁
            hideSelector('#page2 .section-intro');
            hideSelector('#page2 #riskAwareness');
            hideSelector('#page2 .risk-dashboard');
            hideSelector('#page2 .scenario-cards');

            // 第4頁：只列印年齡對應的3個推薦情境，其他隱藏
            try {
                const age = (lastAnalysisData && lastAnalysisData.age) || 40;
                let recommended = [];
                if (age < 36) recommended = ['cancer', 'pelvis', 'heart'];
                else if (age < 51) recommended = ['cancer', 'cart', 'stroke'];
                else recommended = ['longcare', 'transplant', 'icu'];

                // 隱藏Tab按鈕
                hideSelector('#page4 .tab-buttons');

                // 顯示推薦的3個情境，隱藏其餘
                document.querySelectorAll('#page4 .tab-content').forEach(el => {
                    const id = el.id || '';
                    const key = id.endsWith('-tab') ? id.slice(0, -4) : id;
                    if (recommended.includes(key)) {
                        rememberAndSet(el, 'display', 'block');
                    } else {
                        rememberAndSet(el, 'display', 'none');
                    }
                });
            } catch(e) {}

            // 添加列印專用樣式
            const printStyle = document.createElement('style');
            printStyle.id = 'print-style';
            printStyle.textContent = `
                @page {
                    size: A4;
                    margin: 12mm;
                }
                
                @media print {
                    * { 
                        box-sizing: border-box;
                        -webkit-print-color-adjust: exact;
                        print-color-adjust: exact;
                    }
                    
                    body { 
                        background: white !important; 
                        margin: 0;
                        padding: 0;
                        font-size: 11pt !important;
                    }
                    
                    .container {
                        max-width: 100% !important;
                        padding: 0 !important;
                        margin: 0 !important;
                    }
                    
                    header {
                        background: linear-gradient(135deg, #2c3e50, #3498db) !important;
                        padding: 15px 20px !important;
                        margin-bottom: 8mm !important;
                        border-radius: 0 !important;
                        page-break-after: avoid;
                    }
                    
                    header h1 { font-size: 20pt !important; margin-bottom: 5px !important; }
                    header .subtitle { font-size: 11pt !important; }
                    
                    .page { 
                        page-break-after: always;
                        display: block !important;
                        padding: 0 !important;
                        margin: 0 !important;
                        break-inside: avoid;
                    }
                    
                    .card { 
                        box-shadow: none !important; 
                        border: 1px solid #ddd !important;
                        margin-bottom: 6mm !important;
                        padding: 15px !important;
                        page-break-inside: avoid;
                        break-inside: avoid;
                    }
                    
                    .card-title {
                        font-size: 16pt !important;
                        margin-bottom: 12px !important;
                        padding-bottom: 8px !important;
                    }
                    
                    /* 第2頁優化 */
                    .quick-diagnosis {
                        background: linear-gradient(135deg, #667eea 0%, #764ba2 100%) !important;
                        padding: 15px !important;
                        margin-bottom: 8mm !important;
                        page-break-inside: avoid;
                        break-inside: avoid;
                    }
                    
                    .quick-diagnosis h3 { font-size: 14pt !important; margin-bottom: 12px !important; }
                    .quick-diagnosis > div > div { padding: 10px !important; }
                    .quick-diagnosis > div > div > div:first-child { font-size: 9pt !important; }
                    .quick-diagnosis > div > div > div:nth-child(2) { font-size: 18pt !important; }
                    .quick-diagnosis > div > div > div:last-child { font-size: 8pt !important; }
                    
                    .section-intro, .risk-awareness { 
                        font-size: 10pt !important; 
                        margin-bottom: 6mm !important;
                        line-height: 1.4 !important;
                    }
                    
                    /* 列印時隱藏重內容，避免切頁 */
                    .risk-dashboard, .scenario-cards { display: none !important; }
                    
                    .radar-container canvas { 
                        max-height: 200px !important;
                    }
                    
                    .risk-stats-cards {
                        display: flex !important;
                        flex-direction: column !important;
                        gap: 8px !important;
                    }
                    
                    .stat-card {
                        padding: 10px !important;
                        font-size: 10pt !important;
                    }
                    
                    .scenario-grid {
                        display: grid !important;
                        grid-template-columns: repeat(3, 1fr) !important;
                        gap: 8px !important;
                        break-inside: avoid;
                    }
                    
                    .scenario-card {
                        padding: 12px !important;
                        font-size: 9pt !important;
                        break-inside: avoid;
                    }
                    
                    .coverage-gap-section {
                        page-break-inside: avoid;
                        break-inside: avoid;
                    }
                    
                    .gap-dashboard {
                        display: grid !important;
                        grid-template-columns: 0.8fr 1.2fr !important;
                        gap: 10px !important;
                        margin-bottom: 6mm !important;
                        break-inside: avoid;
                    }
                    
                    .gauge-container canvas {
                        max-height: 140px !important;
                    }
                    
                    .gap-bar-item {
                        margin-bottom: 8px !important;
                        font-size: 9pt !important;
                        break-inside: avoid;
                    }
                    
                    /* 第3頁優化 */
                    .priority-sections {
                        display: block !important;
                    }
                    
                    .priority-section {
                        page-break-inside: avoid;
                        break-inside: avoid;
                        margin-bottom: 8mm !important;
                    }
                    
                    .solution-card {
                        page-break-inside: avoid;
                        break-inside: avoid;
                        margin-bottom: 6mm !important;
                        padding: 12px !important;
                        font-size: 10pt !important;
                    }
                    
                    /* 第4頁情境模擬優化 */
                    .tab-buttons { display: none !important; }
                    
                    .tab-content { 
                        display: block !important; 
                        page-break-before: always;
                        page-break-inside: avoid;
                        break-inside: avoid;
                        margin-bottom: 0 !important;
                        padding-top: 5mm !important;
                    }
                    
                    .tab-content:first-of-type {
                        page-break-before: avoid !important;
                    }
                    
                    .tab-content > p {
                        font-size: 11pt !important;
                        margin-bottom: 8px !important;
                    }
                    
                    .chart-grid {
                        display: grid !important;
                        grid-template-columns: 1fr 1fr !important;
                        gap: 10px !important;
                        margin-bottom: 10px !important;
                        page-break-inside: avoid;
                        break-inside: avoid;
                    }
                    
                    .chart-container { 
                        height: 180px !important;
                        page-break-inside: avoid;
                        break-inside: avoid;
                    }
                    
                    .chart-container h4 {
                        font-size: 10pt !important;
                        margin-bottom: 5px !important;
                    }
                    
                    .comparison-grid {
                        display: grid !important;
                        grid-template-columns: repeat(4, 1fr) !important;
                        gap: 8px !important;
                        font-size: 9pt !important;
                        page-break-inside: avoid;
                        break-inside: avoid;
                    }
                    
                    .comparison-item {
                        padding: 10px !important;
                        break-inside: avoid;
                    }
                    
                    .comparison-item h3 {
                        font-size: 10pt !important;
                        margin-bottom: 6px !important;
                    }
                    
                    .comparison-value {
                        font-size: 16pt !important;
                        margin: 6px 0 !important;
                    }
                    
                    .comparison-item p {
                        font-size: 8pt !important;
                        line-height: 1.3 !important;
                    }
                    
                    /* 隱藏不需要的元素 */
                    .submit-btn { display: none !important; }
                    .section-subtitle { font-size: 13pt !important; margin: 8px 0 !important; }
                    
                    /* 緊湊化間距 */
                    h2, h3, h4 { margin-top: 0 !important; }
                    p { margin: 4px 0 !important; }
                }
            `;
            document.head.appendChild(printStyle);

            // 觸發列印
            window.print();

            // 列印完成後恢復原狀
            setTimeout(() => {
                pages.forEach((page, index) => {
                    page.style.display = originalDisplay[index];
                });
                const style = document.getElementById('print-style');
                if (style) style.remove();
                // 還原被隱藏/改動的元素
                restoreDisplayMap.forEach((prev, el) => { try { el.style.display = prev; } catch(e){} });
            }, 1000);
        }
    </script>
</body>
</html>
