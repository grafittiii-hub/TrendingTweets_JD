# TrendingTweets_JD

<!DOCTYPE html>
<html lang="zh-Hant">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>粉絲刷推神器 (Fan Trend Generator)</title>
    <style>
        /* ==================== 新擬物風格設計 ==================== */

        :root {
            --bg-main: #e0e5ec;
            --shadow-light: #ffffff;
            --shadow-dark: #a3b1c6;
            --accent-color: #7b8cde;
            --accent-dark: #5f6fbd;
            --text-primary: #4a5568;
            --text-secondary: #718096;
            --card-bg: #e0e5ec;
        }

        /* 向日葵配色 - 可爱风 */
        [data-theme="sunflower"] {
            --bg-main: #fff8e7;
            --shadow-light: #ffffff;
            --shadow-dark: #d4c5a0;
            --accent-color: #ffb347;
            --accent-dark: #ff9800;
            --text-primary: #5d4e37;
            --text-secondary: #8b7355;
            --card-bg: #fff8e7;
        }

        /* 帅气风 - 红黑配 */
        [data-theme="cool"] {
            --bg-main: #1a1a1a;
            --shadow-light: #2d2d2d;
            --shadow-dark: #0a0a0a;
            --accent-color: #ff3b3b;
            --accent-dark: #cc0000;
            --text-primary: #e8e8e8;
            --text-secondary: #a0a0a0;
            --card-bg: #1a1a1a;
        }

        /* 冷酷风 - 黑白灰 */
        [data-theme="monochrome"] {
            --bg-main: #f0f0f0;
            --shadow-light: #ffffff;
            --shadow-dark: #c0c0c0;
            --accent-color: #555555;
            --accent-dark: #333333;
            --text-primary: #222222;
            --text-secondary: #666666;
            --card-bg: #f0f0f0;
        }

        *, *::before, *::after {
            box-sizing: border-box;
        }

        /* 基礎設置 - 確保適應手機螢幕寬度 */
        html {
            overflow-x: hidden;
            -webkit-text-size-adjust: 100%;
        }

        body {
            font-family: 'Segoe UI', 'PingFang TC', 'Microsoft JhengHei', sans-serif;
            margin: 0;
            padding: 20px;
            background: linear-gradient(135deg, #e0e5ec 0%, #d4dae6 100%);
            color: var(--text-primary);
            min-height: 100vh;
            overflow-x: hidden;
            width: 100%;
            max-width: 100vw;
        }

        .container {
            max-width: 920px;
            width: 100%;
            margin: 0 auto;
            background: var(--card-bg);
            padding: 40px 35px;
            border-radius: 30px;
            box-shadow:
                12px 12px 24px var(--shadow-dark),
                -12px -12px 24px var(--shadow-light);
        }

        h1 {
            color: var(--accent-color);
            text-align: center;
            margin: 0 0 40px 0;
            font-size: 2em;
            font-weight: 700;
            text-shadow: 2px 2px 4px rgba(163, 177, 198, 0.3);
        }

        h2 {
            color: var(--text-primary);
            font-size: 1.2em;
            font-weight: 600;
            margin: 0 0 20px 0;
        }

        /* 輸入與設定區 - 新擬物凹陷效果 */
        .section-box {
            background: var(--card-bg);
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 25px;
            box-shadow:
                inset 6px 6px 12px var(--shadow-dark),
                inset -6px -6px 12px var(--shadow-light);
            overflow: hidden;
            width: 100%;
        }

        label, .checkbox-group label {
            display: block;
            margin-top: 18px;
            margin-bottom: 8px;
            font-weight: 600;
            color: var(--text-primary);
            font-size: 0.95em;
        }

        /* 輸入框 - 新擬物凹陷 */
        input[type="text"], select, textarea {
            width: 100%;
            padding: 14px 18px;
            margin-top: 5px;
            border: none;
            border-radius: 15px;
            background: var(--card-bg);
            box-shadow:
                inset 4px 4px 8px var(--shadow-dark),
                inset -4px -4px 8px var(--shadow-light);
            font-family: inherit;
            font-size: 16px;
            color: var(--text-primary);
            transition: all 0.3s ease;
        }

        input[type="text"]:focus, select:focus, textarea:focus {
            outline: none;
            box-shadow:
                inset 6px 6px 12px var(--shadow-dark),
                inset -6px -6px 12px var(--shadow-light);
        }

        textarea {
            resize: vertical;
            line-height: 1.5;
        }

        /* 快速填入按鈕 - 新擬物凸起 */
        .quick-fill-group, .checkbox-group, .quantity-group {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 12px;
        }

        .quick-fill-group button, .quantity-group button {
            background: var(--card-bg);
            color: var(--accent-color);
            border: none;
            padding: 10px 20px;
            border-radius: 15px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.9em;
            transition: all 0.2s ease;
            box-shadow:
                5px 5px 10px var(--shadow-dark),
                -5px -5px 10px var(--shadow-light);
        }

        .quick-fill-group button:hover, .quantity-group button:hover {
            box-shadow:
                2px 2px 5px var(--shadow-dark),
                -2px -2px 5px var(--shadow-light);
            transform: translateY(1px);
        }

        .quick-fill-group button:active, .quantity-group button:active {
            box-shadow:
                inset 3px 3px 6px var(--shadow-dark),
                inset -3px -3px 6px var(--shadow-light);
        }

        .quantity-group button.active {
            background: linear-gradient(145deg, var(--accent-color), var(--accent-dark));
            color: white;
            box-shadow:
                inset 2px 2px 5px rgba(0,0,0,0.2),
                3px 3px 8px var(--shadow-dark);
        }

        /* 確保推文數目按鈕永遠在一行 */
        .quantity-group {
            flex-wrap: nowrap;
            justify-content: space-between;
        }

        .quantity-group button {
            flex: 1;
            min-width: 0;
        }

        /* 自由描述按鈕 - 彈性佈局保持按鈕原本大小 */
        .free-text-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 12px;
        }

        .free-text-buttons button {
            flex-shrink: 0;
        }

        /* 區塊間距調整 */
        .section-divider {
            margin-top: 28px;
        }

        /* 複選框組 */
        .checkbox-group {
            gap: 10px;
            row-gap: 10px;
        }

        .checkbox-group div {
            flex-grow: 1;
            min-width: 120px;
        }

        .checkbox-group label {
            display: inline-flex;
            align-items: center;
            cursor: pointer;
            font-weight: normal;
            margin: 0;
        }

        input[type="checkbox"], input[type="radio"] {
            margin-right: 8px;
            cursor: pointer;
        }

        /* 主按鈕區 - 新擬物大按鈕 */
        .action-zone {
            text-align: center;
            margin-top: 35px;
        }

        #generate-btn {
            background: linear-gradient(145deg, var(--accent-color), var(--accent-dark));
            color: white;
            padding: 18px 50px;
            font-size: 1.25em;
            font-weight: 700;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            width: 100%;
            transition: all 0.3s ease;
            box-shadow:
                8px 8px 16px var(--shadow-dark),
                -8px -8px 16px var(--shadow-light);
        }

        #generate-btn:hover {
            transform: translateY(-2px);
            box-shadow:
                10px 10px 20px var(--shadow-dark),
                -10px -10px 20px var(--shadow-light);
        }

        #generate-btn:active {
            transform: translateY(0);
            box-shadow:
                inset 4px 4px 8px rgba(0,0,0,0.2),
                inset -2px -2px 6px rgba(255,255,255,0.1);
        }

        /* 結果區 */
        #results-container {
            margin-top: 45px;
            padding-top: 30px;
            margin-bottom: 100px;
        }

        .result-item {
            display: flex;
            align-items: flex-start;
            padding: 10px 12px 10px 8px;
            margin-bottom: 8px;
            border-radius: 15px;
            background: var(--card-bg);
            box-shadow:
                4px 4px 8px var(--shadow-dark),
                -4px -4px 8px var(--shadow-light);
            transition: all 0.2s ease;
        }

        .result-item:hover {
            box-shadow:
                5px 5px 10px var(--shadow-dark),
                -5px -5px 10px var(--shadow-light);
        }

        .result-text {
            flex-grow: 1;
            padding: 0 12px 0 0;
            white-space: pre-wrap;
            word-wrap: break-word;
            font-size: 0.95em;
            line-height: 1.4;
            color: var(--text-primary);
            text-align: left;
            min-height: 20px;
        }

        .result-actions {
            display: flex;
            gap: 8px;
            align-items: flex-start;
            flex-shrink: 0;
            margin-top: 0;
        }

        .result-actions button {
            background: var(--card-bg);
            border: none;
            cursor: pointer;
            font-size: 1.3em;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.2s ease;
            box-shadow:
                3px 3px 6px var(--shadow-dark),
                -3px -3px 6px var(--shadow-light);
            flex-shrink: 0;
        }

        .result-actions button:hover {
            box-shadow:
                2px 2px 4px var(--shadow-dark),
                -2px -2px 4px var(--shadow-light);
            transform: scale(0.98);
        }

        .result-actions button:active {
            box-shadow:
                inset 2px 2px 4px var(--shadow-dark),
                inset -2px -2px 4px var(--shadow-light);
        }

        /* Checkbox 样式优化 */
        .tweet-checkbox {
            margin: 2px 8px 0 4px;
            cursor: pointer;
            flex-shrink: 0;
            width: 16px;
            height: 16px;
        }

        /* 底部操作欄 - 新擬物浮動卡片 */
        .bottom-action-bar {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background: var(--card-bg);
            border-radius: 25px;
            box-shadow:
                10px 10px 20px var(--shadow-dark),
                -10px -10px 20px var(--shadow-light);
            z-index: 998;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
        }

        .bottom-action-bar.expanded {
            width: 400px;
            max-width: calc(100vw - 40px);
        }

        .bottom-action-bar.collapsed {
            width: 65px;
            height: auto;
        }

        .action-bar-header {
            background: linear-gradient(145deg, var(--accent-color), var(--accent-dark));
            color: white;
            padding: 14px 20px;
            cursor: pointer;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-radius: 20px;
            user-select: none;
            font-weight: 600;
        }

        .action-bar-content {
            padding: 18px;
            max-height: 400px;
            opacity: 1;
            transition: opacity 0.3s ease, max-height 0.4s cubic-bezier(0.4, 0, 0.2, 1), padding 0.4s ease;
        }

        .bottom-action-bar.collapsed .action-bar-content {
            max-height: 0;
            opacity: 0;
            padding: 0 18px;
            overflow: hidden;
        }

        .bottom-action-bar.collapsed .action-bar-header {
            writing-mode: vertical-rl;
            text-orientation: mixed;
            text-align: center;
            padding: 20px 14px;
            justify-content: center;
            gap: 8px;
        }

        .bottom-action-bar button {
            padding: 12px 24px;
            border: none;
            border-radius: 15px;
            margin: 8px 0;
            cursor: pointer;
            width: 100%;
            font-weight: 600;
            transition: all 0.2s ease;
            box-shadow:
                4px 4px 8px var(--shadow-dark),
                -4px -4px 8px var(--shadow-light);
        }

        .bottom-action-bar button:hover {
            transform: translateY(-1px);
            box-shadow:
                5px 5px 10px var(--shadow-dark),
                -5px -5px 10px var(--shadow-light);
        }

        .bottom-action-bar button:active {
            transform: translateY(0);
            box-shadow:
                inset 3px 3px 6px var(--shadow-dark),
                inset -3px -3px 6px var(--shadow-light);
        }

        #copy-selected-btn {
            background: linear-gradient(145deg, #7b8cde, #5f6fbd);
            color: white;
        }

        #export-excel-btn {
            background: linear-gradient(145deg, #6dd5a6, #4db88f);
            color: white;
        }

        .toggle-icon {
            font-size: 1.1em;
            transition: transform 0.3s ease;
            margin-left: 6px;
        }

        .bottom-action-bar.collapsed .toggle-icon {
            transform: rotate(90deg);
            margin-left: 0;
        }

        /* 可拖放的回到頂部按鈕 - 新擬物圓形 */
        .back-to-top {
            position: fixed;
            background: var(--card-bg);
            color: var(--accent-color);
            width: 55px;
            height: 55px;
            border-radius: 50%;
            border: none;
            cursor: move;
            font-size: 1.6em;
            font-weight: bold;
            box-shadow:
                8px 8px 16px var(--shadow-dark),
                -8px -8px 16px var(--shadow-light);
            z-index: 999;
            display: none;
            align-items: center;
            justify-content: center;
            transition: opacity 0.3s ease, box-shadow 0.3s ease;
            opacity: 0.85;
            user-select: none;
            top: 0;
            left: 0;
        }

        .back-to-top:hover {
            opacity: 1;
            box-shadow:
                10px 10px 20px var(--shadow-dark),
                -10px -10px 20px var(--shadow-light);
        }

        .back-to-top.dragging {
            opacity: 1;
            transform: scale(1.05);
            cursor: grabbing;
            box-shadow:
                12px 12px 24px var(--shadow-dark),
                -12px -12px 24px var(--shadow-light);
        }

        .back-to-top.show {
            display: flex;
        }

        /* 提示文字 */
        .placeholder-text {
            color: var(--text-secondary);
            font-size: 0.85em;
            margin-top: 8px;
            font-style: italic;
        }

        /* 自定義 Modal - 新擬物 */
        .custom-modal {
            position: fixed;
            inset: 0;
            background-color: rgba(0, 0, 0, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            backdrop-filter: blur(4px);
        }

        .custom-modal-content {
            background: var(--card-bg);
            padding: 35px 40px;
            border-radius: 25px;
            box-shadow:
                15px 15px 30px var(--shadow-dark),
                -15px -15px 30px var(--shadow-light);
            max-width: 420px;
            width: 90%;
            text-align: center;
        }

        .custom-modal-content p {
            margin: 0 0 25px 0;
            color: var(--text-primary);
            font-size: 1.05em;
            line-height: 1.6;
        }

        .custom-modal-content button {
            padding: 12px 35px;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            font-size: 1em;
            font-weight: 600;
            background: linear-gradient(145deg, var(--accent-color), var(--accent-dark));
            color: white;
            box-shadow:
                5px 5px 10px var(--shadow-dark),
                -5px -5px 10px var(--shadow-light);
            transition: all 0.2s ease;
        }

        .custom-modal-content button:hover {
            transform: translateY(-2px);
            box-shadow:
                6px 6px 12px var(--shadow-dark),
                -6px -6px 12px var(--shadow-light);
        }

        .custom-modal-content button:active {
            transform: translateY(0);
            box-shadow:
                inset 3px 3px 6px rgba(0,0,0,0.2),
                inset -2px -2px 4px rgba(255,255,255,0.1);
        }


        /* ==================== 響應式調整 ==================== */

        /* 大螢幕桌面 (1200px+) */
        @media (min-width: 1200px) {
            body {
                padding: 40px;
            }

            .container {
                max-width: 1000px;
                padding: 50px 60px;
            }

            h1 {
                font-size: 2.4em;
                margin-bottom: 50px;
            }

            .section-box {
                padding: 30px;
            }

            .checkbox-group {
                gap: 15px;
            }

            .checkbox-group div {
                min-width: 160px;
            }

            .quick-fill-group button, .quantity-group button {
                padding: 12px 24px;
                font-size: 0.95em;
            }

            .free-text-buttons {
                gap: 12px;
            }

            #generate-btn {
                padding: 20px 60px;
                font-size: 1.35em;
            }

            .result-item {
                padding: 14px 16px 14px 10px;
            }

            .result-text {
                font-size: 1em;
                padding-right: 15px;
            }

            .result-actions button {
                width: 42px;
                height: 42px;
                font-size: 1.4em;
            }

            .bottom-action-bar.expanded {
                width: 450px;
            }

            .theme-switcher button {
                width: 42px;
                height: 42px;
                font-size: 1.35em;
            }

            .help-btn {
                width: 38px;
                height: 38px;
                font-size: 1.35em;
            }
        }

        /* 平板橫向 (1024px - 1199px) */
        @media (min-width: 1024px) and (max-width: 1199px) {
            body {
                padding: 30px;
            }

            .container {
                max-width: 900px;
                padding: 40px 45px;
            }

            h1 {
                font-size: 2.1em;
            }

            .checkbox-group div {
                min-width: 140px;
            }
        }

        /* 平板直向 iPad (768px - 1023px) */
        @media (min-width: 768px) and (max-width: 1023px) {
            body {
                padding: 25px;
            }

            .container {
                max-width: 720px;
                padding: 35px 40px;
            }

            h1 {
                font-size: 1.9em;
                margin-bottom: 35px;
            }

            .section-box {
                padding: 22px;
            }

            .checkbox-group {
                gap: 12px;
            }

            .checkbox-group div {
                min-width: 130px;
                flex: 0 0 calc(33.333% - 10px);
            }

            .quick-fill-group {
                gap: 10px;
            }

            .quick-fill-group button, .quantity-group button {
                padding: 10px 16px;
                font-size: 0.88em;
            }

            .free-text-buttons {
                gap: 10px;
            }

            #generate-btn {
                padding: 16px 45px;
                font-size: 1.2em;
            }

            .bottom-action-bar.expanded {
                width: 380px;
            }

            .result-item {
                padding: 10px 14px 10px 8px;
            }

            .result-actions button {
                width: 38px;
                height: 38px;
                font-size: 1.25em;
            }

            .theme-switcher {
                right: 15px;
                top: 55px;
            }

            .help-btn {
                right: 15px;
                top: 15px;
            }
        }

        /* 大手機/小平板 (601px - 767px) */
        @media (min-width: 601px) and (max-width: 767px) {
            body {
                padding: 20px;
            }

            .container {
                padding: 30px 28px;
            }

            h1 {
                font-size: 1.75em;
                margin-bottom: 30px;
            }

            .section-box {
                padding: 20px;
            }

            .checkbox-group div {
                min-width: 110px;
                flex: 0 0 calc(50% - 8px);
            }

            .quick-fill-group button, .quantity-group button {
                padding: 9px 14px;
                font-size: 0.85em;
            }

            .free-text-buttons {
                gap: 10px;
            }

            #generate-btn {
                padding: 15px 40px;
                font-size: 1.15em;
            }

            .bottom-action-bar.expanded {
                width: 340px;
            }
        }

        /* 手機 (max-width: 600px) */
        @media (max-width: 600px) {
            body {
                padding: 15px;
            }

            .container {
                padding: 25px 20px;
                border-radius: 25px;
                max-width: 100%;
            }

            h1 {
                font-size: 1.6em;
                margin-bottom: 28px;
            }

            .section-box {
                padding: 20px 18px;
                border-radius: 18px;
                margin-bottom: 22px;
            }

            h2 {
                font-size: 1.1em;
                margin-bottom: 18px;
            }

            label {
                font-size: 0.95em;
                margin-top: 16px;
            }

            input[type="text"], select, textarea {
                padding: 14px 16px;
                border-radius: 14px;
                font-size: 16px; /* 防止iOS縮放 */
            }

            .checkbox-group {
                gap: 10px;
                row-gap: 10px;
            }

            .checkbox-group div {
                min-width: 100px;
                flex: 0 0 calc(50% - 6px);
            }

            .checkbox-group label {
                font-size: 0.9em;
            }

            .quick-fill-group {
                gap: 10px;
                flex-wrap: wrap;
            }

            .quick-fill-group button, .quantity-group button {
                padding: 10px 14px;
                font-size: 0.85em;
                border-radius: 14px;
            }

            .quantity-group {
                gap: 8px;
            }

            .free-text-buttons {
                gap: 8px;
                margin-top: 12px;
            }

            .placeholder-text {
                font-size: 0.85em;
                line-height: 1.5;
            }

            .action-zone {
                margin-top: 28px;
            }

            #generate-btn {
                font-size: 1.15em;
                padding: 16px 30px;
                border-radius: 18px;
            }

            #results-container {
                margin-top: 38px;
                padding-top: 28px;
                margin-bottom: 130px;
            }

            .result-item {
                padding: 10px 12px 10px 8px;
                border-radius: 14px;
                margin-bottom: 8px;
            }

            .result-text {
                padding: 0 10px 0 0;
                font-size: 0.92em;
                line-height: 1.4;
            }

            .result-actions {
                gap: 6px;
            }

            .result-actions button {
                width: 34px;
                height: 34px;
                font-size: 1.2em;
            }

            .tweet-checkbox {
                margin: 2px 8px 0 4px;
                width: 16px;
                height: 16px;
            }

            .bottom-action-bar {
                bottom: 15px;
                right: 15px;
            }

            .bottom-action-bar.expanded {
                width: calc(100vw - 30px);
                right: 15px;
            }

            .bottom-action-bar.collapsed {
                right: 15px;
                width: 60px;
            }

            .action-bar-header {
                padding: 14px 18px;
                font-size: 0.95em;
            }

            .action-bar-content {
                padding: 16px;
            }

            .bottom-action-bar button {
                padding: 12px 22px;
                font-size: 0.95em;
            }

            .back-to-top {
                width: 50px;
                height: 50px;
                font-size: 1.4em;
            }

            .custom-modal-content {
                padding: 30px 28px;
                border-radius: 22px;
                width: 90%;
            }

            .custom-modal-content p {
                font-size: 1em;
            }

            .custom-modal-content button {
                padding: 12px 30px;
                font-size: 1em;
            }
        }

        /* 超小手機 (max-width: 380px) */
        @media (max-width: 380px) {
            body {
                padding: 12px;
            }

            .container {
                padding: 20px 16px;
                border-radius: 22px;
            }

            h1 {
                font-size: 1.4em;
                margin-bottom: 22px;
            }

            .section-box {
                padding: 16px 14px;
                border-radius: 16px;
            }

            h2 {
                font-size: 1.05em;
            }

            .checkbox-group div {
                flex: 0 0 100%;
            }

            .quick-fill-group button, .quantity-group button {
                padding: 8px 12px;
                font-size: 0.8em;
            }

            .free-text-buttons {
                gap: 8px;
            }

            #generate-btn {
                font-size: 1.05em;
                padding: 14px 24px;
            }

            .result-actions button {
                width: 32px;
                height: 32px;
                font-size: 1.1em;
            }

            .bottom-action-bar {
                bottom: 12px;
                right: 12px;
            }

            .bottom-action-bar.expanded {
                width: calc(100vw - 24px);
                right: 12px;
            }

            .bottom-action-bar.collapsed {
                right: 12px;
                width: 55px;
            }
        }

        /* 語言切換按鈕 */
        .lang-switcher {
            position: fixed;
            left: 12px;
            top: 12px;
            background: var(--card-bg);
            border-radius: 14px;
            padding: 4px 6px;
            box-shadow:
                4px 4px 8px var(--shadow-dark),
                -4px -4px 8px var(--shadow-light);
            z-index: 1000;
            display: flex;
            gap: 4px;
            opacity: 0.4;
            transition: all 0.3s ease;
        }

        .lang-switcher.expanded {
            opacity: 1;
        }

        .lang-switcher button {
            background: var(--card-bg);
            color: var(--text-secondary);
            border: none;
            padding: 4px 8px;
            border-radius: 10px;
            cursor: pointer;
            font-weight: 600;
            font-size: 0.7em;
            transition: all 0.3s ease;
            box-shadow:
                2px 2px 4px var(--shadow-dark),
                -2px -2px 4px var(--shadow-light);
            opacity: 0;
            max-width: 0;
            overflow: hidden;
            padding: 0;
        }

        .lang-switcher button.active {
            background: linear-gradient(145deg, var(--accent-color), var(--accent-dark));
            color: white;
            box-shadow:
                inset 2px 2px 4px rgba(0,0,0,0.2),
                2px 2px 4px var(--shadow-dark);
            opacity: 1;
            max-width: 45px;
            padding: 4px 8px;
        }

        .lang-switcher.expanded button {
            opacity: 1;
            max-width: 60px;
            padding: 4px 8px;
        }

        .lang-switcher button:hover {
            transform: translateY(-1px);
        }

        /* 標題容器 */
        .header-container {
            position: relative;
            text-align: center;
        }

        /* 幫助按鈕 */
        .help-btn {
            position: fixed;
            right: 12px;
            top: 12px;
            background: var(--card-bg);
            color: var(--accent-color);
            border: none;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            cursor: pointer;
            font-weight: bold;
            font-size: 1.2em;
            box-shadow:
                3px 3px 6px var(--shadow-dark),
                -3px -3px 6px var(--shadow-light);
            z-index: 1000;
            opacity: 0.3;
            transition: all 0.3s ease;
        }

        .help-btn:hover {
            opacity: 1;
            transform: scale(1.1);
        }

        /* 主題切換按鈕 */
        .theme-switcher {
            position: fixed;
            right: 12px;
            top: 52px;
            background: var(--card-bg);
            border-radius: 20px;
            padding: 6px;
            box-shadow:
                4px 4px 8px var(--shadow-dark),
                -4px -4px 8px var(--shadow-light);
            z-index: 1000;
            display: flex;
            flex-direction: column;
            gap: 6px;
            opacity: 0.4;
            transition: all 0.3s ease;
        }

        .theme-switcher:hover {
            opacity: 1;
        }

        .theme-switcher button {
            background: var(--card-bg);
            border: none;
            width: 36px;
            height: 36px;
            border-radius: 50%;
            cursor: pointer;
            font-size: 1.2em;
            transition: all 0.2s ease;
            box-shadow:
                2px 2px 4px var(--shadow-dark),
                -2px -2px 4px var(--shadow-light);
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .theme-switcher button.active {
            box-shadow:
                inset 2px 2px 4px var(--shadow-dark),
                inset -2px -2px 4px var(--shadow-light);
            transform: scale(0.95);
        }

        .theme-switcher button:hover {
            transform: scale(1.05);
        }


        /* 教學彈窗 */
        .tutorial-overlay {
            position: fixed;
            inset: 0;
            background-color: rgba(0, 0, 0, 0.6);
            display: none;
            align-items: center;
            justify-content: center;
            z-index: 10000;
            backdrop-filter: blur(4px);
        }

        .tutorial-overlay.show {
            display: flex;
        }

        .tutorial-content {
            background: var(--card-bg);
            padding: 35px 40px;
            border-radius: 25px;
            box-shadow:
                15px 15px 30px var(--shadow-dark),
                -15px -15px 30px var(--shadow-light);
            max-width: 600px;
            width: 90%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .tutorial-content h2 {
            color: var(--accent-color);
            margin: 0 0 20px 0;
            text-align: center;
        }

        .tutorial-content .tip {
            margin: 15px 0;
            padding: 12px 15px;
            background: var(--card-bg);
            border-radius: 15px;
            box-shadow:
                inset 3px 3px 6px var(--shadow-dark),
                inset -3px -3px 6px var(--shadow-light);
        }

        .tutorial-content .tip strong {
            color: var(--accent-color);
            display: block;
            margin-bottom: 5px;
        }

        .tutorial-content button {
            width: 100%;
            margin-top: 20px;
            padding: 12px 35px;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            font-size: 1em;
            font-weight: 600;
            background: linear-gradient(145deg, var(--accent-color), var(--accent-dark));
            color: white;
            box-shadow:
                5px 5px 10px var(--shadow-dark),
                -5px -5px 10px var(--shadow-light);
            transition: all 0.2s ease;
        }

        .tutorial-content button:hover {
            transform: translateY(-2px);
        }

        .tutorial-content label {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-top: 15px;
            font-size: 0.9em;
            color: var(--text-secondary);
            cursor: pointer;
        }

        .tutorial-content label input {
            margin-right: 8px;
        }

        /* 響應式 - 固定元素（語言、主題、教學） */
        @media (min-width: 1200px) {
            .lang-switcher {
                left: 20px;
                top: 20px;
            }

            .help-btn {
                right: 20px;
                top: 20px;
            }

            .theme-switcher {
                right: 20px;
                top: 65px;
            }

            .tutorial-content {
                max-width: 650px;
                padding: 40px 50px;
            }
        }

        @media (min-width: 768px) and (max-width: 1023px) {
            .tutorial-content {
                max-width: 550px;
                padding: 30px 35px;
            }
        }

        @media (max-width: 600px) {
            .lang-switcher {
                left: 8px;
                top: 8px;
                padding: 3px 5px;
                gap: 3px;
            }

            .lang-switcher button {
                padding: 3px 6px;
                font-size: 0.65em;
            }

            .lang-switcher button.active {
                max-width: 40px;
                padding: 3px 6px;
            }

            .lang-switcher.expanded button {
                max-width: 45px;
                padding: 3px 6px;
            }

            .help-btn {
                right: 8px;
                top: 8px;
                width: 28px;
                height: 28px;
                font-size: 1em;
            }

            .theme-switcher {
                right: 8px;
                top: 42px;
                padding: 4px;
                gap: 4px;
            }

            .theme-switcher button {
                width: 30px;
                height: 30px;
                font-size: 1em;
            }

            .tutorial-content {
                padding: 25px 22px;
                max-width: 95%;
                max-height: 85vh;
            }

            .tutorial-content h2 {
                font-size: 1.1em;
            }

            .tutorial-content .tip {
                padding: 10px 12px;
                font-size: 0.9em;
            }
        }

        @media (max-width: 380px) {
            .lang-switcher {
                left: 6px;
                top: 6px;
            }

            .lang-switcher button {
                font-size: 0.6em;
            }

            .help-btn {
                right: 6px;
                top: 6px;
                width: 26px;
                height: 26px;
            }

            .theme-switcher {
                right: 6px;
                top: 38px;
            }

            .theme-switcher button {
                width: 26px;
                height: 26px;
                font-size: 0.9em;
            }

            .tutorial-content {
                padding: 20px 18px;
            }

            .tutorial-content .tip {
                padding: 8px 10px;
                font-size: 0.85em;
            }
        }
    </style>
</head>
<body>

<!-- 語言切換按鈕 -->
<div class="lang-switcher">
    <button class="lang-btn active" data-lang="zh" onclick="switchLanguage('zh')">中</button>
    <button class="lang-btn" data-lang="en" onclick="switchLanguage('en')">EN</button>
    <button class="lang-btn" data-lang="th" onclick="switchLanguage('th')">ไทย</button>
</div>

<!-- 幫助按鈕 -->
<button class="help-btn" onclick="showTutorial()" title="查看教學">?</button>

<!-- 主題切換按鈕 -->
<div class="theme-switcher">
    <button class="theme-btn active" data-theme="default" onclick="switchTheme('default')" title="原色">🎨</button>
    <button class="theme-btn" data-theme="sunflower" onclick="switchTheme('sunflower')" title="向日葵">🌻</button>
    <button class="theme-btn" data-theme="cool" onclick="switchTheme('cool')" title="帥氣">🔥</button>
    <button class="theme-btn" data-theme="monochrome" onclick="switchTheme('monochrome')" title="冷酷">⚫</button>
</div>

<div class="container">
    <div class="header-container">
        <h1 data-i18n="title">FC刷推生成器</h1>
    </div>

    <div class="section-box">
        <h2 data-i18n="inputArea">輸入區域</h2>

        <label for="mandatory-text" data-i18n="mandatoryLabel">1. 必須包括的字句及 Hashtag：</label>
        <textarea id="mandatory-text" rows="3" data-i18n="mandatoryPlaceholder" placeholder="#DareYouToDeath"></textarea>
        <div class="quick-fill-group" style="margin-top: 10px;">
            <button onclick="toggleTextInField('mandatory-text', '#DareYouToDeath')">#DareYouToDeath</button>
            <button onclick="toggleTextInField('mandatory-text', '#DareYouToDeathEP1')">#DareYouToDeathEP1</button>
            <button onclick="toggleTextInField('mandatory-text', '#จุงดัง')">#จุงดัง</button>
            <button onclick="toggleTextInField('mandatory-text', '#JoongDunk')">#JoongDunk</button>
        </div>
        <div style="display:flex; gap:20px; margin-top:10px;">
            <label style="margin-top:0;">
                <input type="radio" name="position" value="prefix" data-i18n="positionPrefix"> <span data-i18n="positionPrefix">放在開頭</span>
            </label>
            <label style="margin-top:0;">
                <input type="radio" name="position" value="suffix" checked data-i18n="positionSuffix"> <span data-i18n="positionSuffix">放在結尾</span>
            </label>
        </div>

        <label for="free-text" class="section-divider" data-i18n="freeTextLabel">2. 自由描述/形容詞 (可選留空)：</label>
        <textarea id="free-text" rows="4" data-i18n="freeTextPlaceholder" placeholder="輸入 CP 名、劇名或角色名 (例如: JoongDunk, JadeKamin, ...)"></textarea>
        <div class="placeholder-text" data-i18n="freeTextHint">此處詞彙會被隨機插入，確保內容與您的主題相關。點選下方詞語可同時勾選多個，以逗號分隔。再次點選可移除。</div>

        <!-- 自由描述按鈕 -->
        <div class="free-text-buttons">
            <button onclick="toggleTextInField('free-text', 'JoongDunk')">JoongDunk</button>
            <button onclick="toggleTextInField('free-text', 'Joong')">Joong</button>
            <button onclick="toggleTextInField('free-text', 'Dunk')">Dunk</button>
            <button onclick="toggleTextInField('free-text', 'JadeKamin')">JadeKamin</button>
            <button onclick="toggleTextInField('free-text', 'Jade')">Jade</button>
            <button onclick="toggleTextInField('free-text', 'Kamin')">Kamin</button>
            <button onclick="toggleTextInField('free-text', 'Dare You To Death')">Dare You To Death</button>
            <button onclick="toggleTextInField('free-text', 'จุงดัง')">จุงดัง</button>
        </div>
    </div>

    <div class="section-box">
        <h2 data-i18n="paramSettings">參數設定</h2>

        <label data-i18n="themesLabel">1. 內容方向 (Themes)：</label>
        <div class="checkbox-group">
            <div><label><input type="checkbox" name="theme" value="series" checked data-i18n="themeSeries"> <span data-i18n="themeSeries">劇集/作品</span></label></div>
            <div><label><input type="checkbox" name="theme" value="chemistry" checked data-i18n="themeChemistry"> <span data-i18n="themeChemistry">兩人的化學反應</span></label></div>
            <div><label><input type="checkbox" name="theme" value="visuals" data-i18n="themeVisuals"> <span data-i18n="themeVisuals">外貌打扮</span></label></div>
            <div><label><input type="checkbox" name="theme" value="hype" checked data-i18n="themeHype"> <span data-i18n="themeHype">純支持/打氣</span></label></div>
            <div><label><input type="checkbox" name="theme" value="ost" data-i18n="themeOst"> <span data-i18n="themeOst">OST/主題曲</span></label></div>
            <div><label><input type="checkbox" name="theme" value="call_to_action" data-i18n="themeCallToAction"> <span data-i18n="themeCallToAction">呼籲</span></label></div>
        </div>

        <div style="display: flex; gap: 20px; margin-top: 12px; flex-wrap: wrap;">
            <div style="flex: 1; min-width: 180px;">
                <label data-i18n="outputLangLabel">2. 輸出語言：</label>
                <select id="output-lang">
                    <option value="en" data-i18n="outputLangEn">English (英文)</option>
                    <option value="th" data-i18n="outputLangTh">Thai (泰文)</option>
                    <option value="mix" data-i18n="outputLangMix">Mix (混合)</option>
                </select>
            </div>
            <div style="flex: 1; min-width: 180px;">
                <label data-i18n="emojiLabel">3. Emoji 設定：</label>
                <label style="margin-top: 5px;"><input type="checkbox" id="include-emoji" checked data-i18n="emojiInclude"> <span data-i18n="emojiInclude">包含 Emoji</span></label>
            </div>
        </div>

        <label data-i18n="quantityLabel">4. 生成推文數目：</label>
        <div class="quantity-group" id="quantity-options">
            <button data-qty="25" class="active">25</button>
            <button data-qty="50">50</button>
            <button data-qty="100">100</button>
            <button data-qty="200">200</button>
            <input type="hidden" id="selected-qty" value="25">
        </div>
    </div>

    <div class="action-zone">
        <button id="generate-btn" data-i18n="generateBtn">一鍵生成 X Post 內容</button>
    </div>

    <div id="results-container" style="display:none;">
        <h2 id="results-title" data-i18n="resultsTitle" style="text-align: center; color: var(--accent-color); font-size: 1.5em; margin-bottom: 25px;">生成結果</h2>
        <div id="tweets-list"></div>
    </div>

</div>

<!-- 可拖放的回到頂部按鈕 -->
<button class="back-to-top" id="back-to-top">↑</button>

<!-- 底部操作欄 -->
<div class="bottom-action-bar expanded" id="bottom-bar" style="display:none;">
    <div class="action-bar-header" onclick="toggleActionBar()">
        <span id="bar-title" data-i18n="toolsTitle">操作工具</span>
        <span class="toggle-icon" id="toggle-icon">▼</span>
    </div>
    <div class="action-bar-content">
        <p id="generation-status" style="margin: 0 0 12px 0; color: var(--text-secondary); font-size: 0.9em;"></p>
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 8px; margin-bottom: 12px;">
            <button id="copy-selected-btn" style="margin: 0;" data-i18n="copyBtn">📋 複製</button>
            <button id="export-excel-btn" style="margin: 0;" data-i18n="csvBtn">📊 CSV</button>
            <button id="export-txt-btn" style="margin: 0;" data-i18n="txtBtn">📝 TXT</button>
        </div>
        <div style="display: flex; gap: 8px; margin-bottom: 12px;">
            <button id="invert-selection-btn" style="margin: 0;">🔄 反選</button>
        </div>
        <label style="display: block;">
            <input type="checkbox" id="select-all-checkbox" checked data-i18n="selectAll"> <span data-i18n="selectAll">全選/取消全選</span>
        </label>
        <p style="margin: 8px 0 0 0; color: var(--text-secondary); font-size: 0.85em; text-align: center;" id="selection-count">已選擇 0 條</p>
    </div>
</div>

<!-- 教學彈窗 -->
<div class="tutorial-overlay" id="tutorial-overlay">
    <div class="tutorial-content">
        <h2 data-i18n="tutorialTitle">📖 快速操作指南</h2>
        <div class="tip">
            <strong data-i18n="tutorialThemeTitle">🎨 主題切換</strong>
            <span data-i18n="tutorialThemeDesc">右上角可切換4種配色主題：原色、向日葵（可愛風）、帥氣風（紅黑）、冷酷風（灰階）</span>
        </div>
        <div class="tip">
            <strong data-i18n="tutorialLangTitle">🌐 語言切換</strong>
            <span data-i18n="tutorialLangDesc">左上角可切換中/英/泰文界面。滾動頁面時語言按鈕會自動收合。</span>
        </div>
        <div class="tip">
            <strong data-i18n="tutorialBtnTitle">↑ 置頂按鈕</strong>
            <span data-i18n="tutorialBtnDesc">右下角的圓形按鈕可以自由拖動到任意位置。單擊：跳到生成結果。雙擊：回到頁面最頂部</span>
        </div>
        <div class="tip">
            <strong data-i18n="tutorialBatchTitle">🔄 批量操作</strong>
            <span data-i18n="tutorialBatchDesc">"反選"可快速選中未勾選的推文。底部顯示已選擇的推文數量。</span>
        </div>
        <div class="tip">
            <strong data-i18n="tutorialExportTitle">💾 導出功能</strong>
            <span data-i18n="tutorialExportDesc">支持複製到剪貼簿、導出CSV（Excel）和TXT文件三種格式。</span>
        </div>
        <label>
            <input type="checkbox" id="dont-show-tutorial">
            <span data-i18n="tutorialDontShow">不再顯示此教學</span>
        </label>
        <button onclick="closeTutorial()" data-i18n="tutorialGotIt">知道了</button>
    </div>
</div>

<script>
    // --- 主題切換 ---
    function switchTheme(theme) {
        if (theme === 'default') {
            document.documentElement.removeAttribute('data-theme');
        } else {
            document.documentElement.setAttribute('data-theme', theme);
        }

        // 更新按鈕狀態
        document.querySelectorAll('.theme-btn').forEach(btn => {
            btn.classList.remove('active');
            if (btn.dataset.theme === theme) {
                btn.classList.add('active');
            }
        });

        // 保存主題偏好
        try {
            localStorage.setItem('preferredTheme', theme); // eslint-disable-line no-restricted-globals
        } catch (e) {
            // localStorage 不可用时静默失败
        }
    }

    // --- 教學彈窗 ---
    function showTutorial() {
        const overlay = document.getElementById('tutorial-overlay');
        if (overlay) {
            overlay.classList.add('show');
        }
    }

    function closeTutorial() {
        const overlay = document.getElementById('tutorial-overlay');
        const dontShow = document.getElementById('dont-show-tutorial');

        if (overlay) {
            overlay.classList.remove('show');
        }

        if (dontShow && dontShow.checked) {
            try {
                localStorage.setItem('hideTutorial', 'true'); // eslint-disable-line no-restricted-globals
            } catch (e) {
                // localStorage 不可用时静默失败
            }
        }
    }

    // --- 批量操作 ---
    function invertSelection() {
        document.querySelectorAll('.tweet-checkbox').forEach(cb => {
            cb.checked = !cb.checked;
        });
        updateSelectionCount();
    }

    function updateSelectionCount() {
        const checkedCount = document.querySelectorAll('.tweet-checkbox:checked').length;
        const totalCount = document.querySelectorAll('.tweet-checkbox').length;
        const countDisplay = document.getElementById('selection-count');

        if (countDisplay) {
            countDisplay.textContent = `已選擇 ${checkedCount} / ${totalCount} 條`;
        }
    }


    // --- 多語言翻譯 ---
    const TRANSLATIONS = {
        zh: {
            title: "FC刷推生成器",
            inputArea: "輸入區域",
            mandatoryLabel: "1. 必須包括的字句及 Hashtag：",
            mandatoryPlaceholder: "#DareYouToDeath",
            positionPrefix: "放在開頭",
            positionSuffix: "放在結尾",
            freeTextLabel: "2. 自由描述/形容詞 (可選留空)：",
            freeTextPlaceholder: "輸入 CP 名、劇名或角色名 (例如: JoongDunk, JadeKamin, ...)",
            freeTextHint: "此處詞彙會被隨機插入，確保內容與您的主題相關。點選下方詞語可同時勾選多個，以逗號分隔。再次點選可移除。",
            paramSettings: "參數設定",
            themesLabel: "1. 內容方向 (Themes)：",
            themeSeries: "劇集/作品",
            themeChemistry: "兩人的化學反應",
            themeVisuals: "外貌打扮",
            themeHype: "純支持/打氣",
            themeOst: "OST/主題曲",
            themeCallToAction: "呼籲",
            outputLangLabel: "2. 輸出語言：",
            outputLangEn: "English (英文)",
            outputLangTh: "Thai (泰文)",
            outputLangMix: "Mix (混合)",
            emojiLabel: "3. Emoji 設定：",
            emojiInclude: "包含 Emoji",
            quantityLabel: "4. 生成推文數目：",
            generateBtn: "一鍵生成 X Post 內容",
            resultsTitle: "生成結果",
            toolsTitle: "操作工具",
            toolsTitleShort: "工具",
            copyBtn: "複製",
            csvBtn: "CSV",
            txtBtn: "TXT",
            selectAll: "全選/取消全選",
            msgSelectTheme: "請至少勾選一個「內容方向」。",
            msgNegativeWords: "偵測到「自由描述」中可能包含負面詞彙，為確保內容正面，請修改您的輸入。",
            msgNoCorpus: "選擇的語言和主題組合沒有可用的語料庫，請嘗試不同組合。",
            msgSelectTweets: "請先勾選您想導出的推文！",
            msgSelectCopy: "請先勾選您想複製的推文！",
            msgCopySuccess: "成功複製 {count} 則推文到剪貼簿！",
            msgCopyFailed: "複製失敗，請手動複製。",
            msgExportSuccess: "成功導出 {count} 則推文到 Excel (CSV 格式)！",
            msgExportTxtSuccess: "成功導出 {count} 則推文到 TXT 文件！",
            msgGenSuccess: "成功生成 {count} 則推文",
            confirm: "確定",
            tutorialTitle: "📖 快速操作指南",
            tutorialThemeTitle: "🎨 主題切換",
            tutorialThemeDesc: "右上角可切換4種配色主題：原色、向日葵（可愛風）、帥氣風（紅黑）、冷酷風（灰階）",
            tutorialLangTitle: "🌐 語言切換",
            tutorialLangDesc: "左上角可切換中/英/泰文界面。滾動頁面時語言按鈕會自動收合。",
            tutorialBtnTitle: "↑ 置頂按鈕",
            tutorialBtnDesc: "右下角的圓形按鈕可以自由拖動到任意位置。單擊：跳到生成結果。雙擊：回到頁面最頂部",
            tutorialBatchTitle: "🔄 批量操作",
            tutorialBatchDesc: "「反選」可快速選中未勾選的推文。底部顯示已選擇的推文數量。",
            tutorialExportTitle: "💾 導出功能",
            tutorialExportDesc: "支持複製到剪貼簿、導出CSV（Excel）和TXT文件三種格式。",
            tutorialDontShow: "不再顯示此教學",
            tutorialGotIt: "知道了"
        },
        en: {
            title: "Fan Tweet Generator",
            inputArea: "Input Area",
            mandatoryLabel: "1. Required Text & Hashtags:",
            mandatoryPlaceholder: "#DareYouToDeath",
            positionPrefix: "Place at Start",
            positionSuffix: "Place at End",
            freeTextLabel: "2. Free Description/Keywords (Optional):",
            freeTextPlaceholder: "Enter CP name, series name or character name (e.g.: JoongDunk, JadeKamin, ...)",
            freeTextHint: "These keywords will be randomly inserted. Click the words below to select multiple (comma-separated). Click again to remove.",
            paramSettings: "Parameter Settings",
            themesLabel: "1. Content Themes:",
            themeSeries: "Series/Work",
            themeChemistry: "Chemistry",
            themeVisuals: "Visuals/Style",
            themeHype: "Support/Hype",
            themeOst: "OST/Theme Song",
            themeCallToAction: "Call to Action",
            outputLangLabel: "2. Output Language:",
            outputLangEn: "English",
            outputLangTh: "Thai",
            outputLangMix: "Mix",
            emojiLabel: "3. Emoji Settings:",
            emojiInclude: "Include Emoji",
            quantityLabel: "4. Number of Tweets:",
            generateBtn: "Generate X Posts",
            resultsTitle: "Generated Results",
            toolsTitle: "Tools",
            toolsTitleShort: "Tools",
            copyBtn: "Copy",
            csvBtn: "CSV",
            txtBtn: "TXT",
            selectAll: "Select All / Deselect All",
            msgSelectTheme: "Please select at least one content theme.",
            msgNegativeWords: "Negative words detected in your description. Please modify your input to ensure positive content.",
            msgNoCorpus: "No templates available for selected language and theme combination. Please try different settings.",
            msgSelectTweets: "Please select tweets to export!",
            msgSelectCopy: "Please select tweets to copy!",
            msgCopySuccess: "Successfully copied {count} tweets to clipboard!",
            msgCopyFailed: "Copy failed, please copy manually.",
            msgExportSuccess: "Successfully exported {count} tweets to CSV format!",
            msgExportTxtSuccess: "Successfully exported {count} tweets to TXT file!",
            msgGenSuccess: "Successfully generated {count} tweets",
            confirm: "OK",
            tutorialTitle: "📖 Quick Guide",
            tutorialThemeTitle: "🎨 Theme Switch",
            tutorialThemeDesc: "Switch between 4 color themes in the top right: Default, Sunflower (Cute), Cool (Red & Black), Monochrome (Grayscale)",
            tutorialLangTitle: "🌐 Language Switch",
            tutorialLangDesc: "Switch between Chinese/English/Thai in the top left. Language buttons auto-collapse when scrolling.",
            tutorialBtnTitle: "↑ Scroll Button",
            tutorialBtnDesc: "The round button in the bottom right can be freely dragged anywhere. Single click: Jump to results. Double click: Back to top",
            tutorialBatchTitle: "🔄 Batch Operations",
            tutorialBatchDesc: "Use 'Invert' to quickly select unchecked tweets. The bottom shows selected count.",
            tutorialExportTitle: "💾 Export Options",
            tutorialExportDesc: "Supports copying to clipboard, exporting to CSV (Excel) and TXT file formats.",
            tutorialDontShow: "Don't show this again",
            tutorialGotIt: "Got it"
        },
        th: {
            title: "เครื่องมือสร้างทวีตแฟนคลับ",
            inputArea: "พื้นที่ป้อนข้อมูล",
            mandatoryLabel: "1. ข้อความและแฮชแท็กที่จำเป็น:",
            mandatoryPlaceholder: "#DareYouToDeath",
            positionPrefix: "วางไว้ที่ต้น",
            positionSuffix: "วางไว้ที่ท้าย",
            freeTextLabel: "2. คำอธิบาย/คีย์เวิร์ดเสริม (ตัวเลือก):",
            freeTextPlaceholder: "ใส่ชื่อคู่จิ้น ชื่อซีรีส์ หรือชื่อตัวละคร (เช่น: JoongDunk, JadeKamin, ...)",
            freeTextHint: "คีย์เวิร์ดเหล่านี้จะถูกสุ่มแทรกเข้าไป คลิกคำด้านล่างเพื่อเลือกหลายคำ (คั่นด้วยจุลภาค) คลิกอีกครั้งเพื่อลบออก",
            paramSettings: "การตั้งค่าพารามิเตอร์",
            themesLabel: "1. ธีมเนื้อหา:",
            themeSeries: "ซีรีส์/ผลงาน",
            themeChemistry: "เคมี",
            themeVisuals: "ภาพลักษณ์/สไตล์",
            themeHype: "ซัพพอร์ต/ให้กำลังใจ",
            themeOst: "เพลงประกอบ",
            themeCallToAction: "เรียกร้อง",
            outputLangLabel: "2. ภาษาผลลัพธ์:",
            outputLangEn: "อังกฤษ",
            outputLangTh: "ไทย",
            outputLangMix: "ผสม",
            emojiLabel: "3. การตั้งค่าอีโมจิ:",
            emojiInclude: "รวมอีโมจิ",
            quantityLabel: "4. จำนวนทวีต:",
            generateBtn: "สร้างโพสต์ X",
            resultsTitle: "ผลลัพธ์ที่สร้าง",
            toolsTitle: "เครื่องมือ",
            toolsTitleShort: "เครื่องม���อ",
            copyBtn: "คัดลอก",
            csvBtn: "CSV",
            txtBtn: "TXT",
            selectAll: "เลือกทั้งหมด / ยกเลิก",
            msgSelectTheme: "โปรดเลือกธีมเนื้อหาอย่างน้อยหนึ่งธีม",
            msgNegativeWords: "ตรวจพบคำลบในคำอธิบายของคุณ โปรดแก้ไขข้อมูลเพื่อให้เนื้อหาเป็นบวก",
            msgNoCorpus: "ไม่มีเทมเพลตสำหรับภาษาและธีมที่เลือก โปรดลองตั้งค่าอื่น",
            msgSelectTweets: "โปรดเลือกทวีตเพื่อส่งออก!",
            msgSelectCopy: "โปรดเลือกทวีตเพื่อคัดลอก!",
            msgCopySuccess: "คัดลอก {count} ทวีตไปยังคลิปบอร์ดสำเร็จ!",
            msgCopyFailed: "การคัดลอกล้มเหลว โปรดคัดลอกด้วยตนเอง",
            msgExportSuccess: "ส่งออก {count} ทวีตเป็นรูปแบบ CSV สำเร็จ!",
            msgExportTxtSuccess: "ส่งออก {count} ทวีตเป็นไฟล์ TXT สำเร็จ!",
            msgGenSuccess: "สร้าง {count} ทวีตสำเร็จ",
            confirm: "ตกลง",
            tutorialTitle: "📖 คู่มือใช้งานด่วน",
            tutorialThemeTitle: "🎨 เปลี่ยนธีม",
            tutorialThemeDesc: "เปลี่ยน 4 ธีมสีที่มุมขวาบน: ต้นฉบับ, ดอกทานตะวัน (น่ารัก), เท่ (แดง-ดำ), โมโนโครม (เทา)",
            tutorialLangTitle: "🌐 เปลี่ยนภาษา",
            tutorialLangDesc: "เปลี่ยนภาษาจีน/อังกฤษ/ไทยที่มุมซ้ายบน ปุ่มภาษาจะย่อเมื่อเลื่อนหน้า",
            tutorialBtnTitle: "↑ ปุ่มเลื่อน",
            tutorialBtnDesc: "ปุ่มกลมที่มุมขวาล่างสามารถลากไปวางที่ไหนก็ได้ คลิกเดียว: ไปผลลัพธ์ ดับเบิลคลิก: กลับด้านบน",
            tutorialBatchTitle: "🔄 การดำเนินการเป็นกลุ่ม",
            tutorialBatchDesc: "ใช้ 'สลับการเลือก' เพื่อเลือกทวีตที่ไม่ได้ติ๊ก ด้านล่างแสดงจำนวนที่เลือก",
            tutorialExportTitle: "💾 ตัวเลือกส่งออก",
            tutorialExportDesc: "รองรับการคัดลอกไปคลิปบอร์ด ส่งออกเป็น CSV (Excel) และไฟล์ TXT",
            tutorialDontShow: "ไม่ต้องแสดงอีก",
            tutorialGotIt: "เข้าใจแล้ว"
        }
    };

    let currentLang = 'zh'; // 預設語言

    let langSwitcherTimeout;
    let pageIdleTimeout;

    // 切換語言函數
    function switchLanguage(lang) {
        currentLang = lang;

        // 更新按鈕狀態
        document.querySelectorAll('.lang-btn').forEach(btn => {
            btn.classList.remove('active');
            if (btn.dataset.lang === lang) {
                btn.classList.add('active');
            }
        });

        // 更新所有翻譯文本
        document.querySelectorAll('[data-i18n]').forEach(el => {
            const key = el.dataset.i18n;
            if (TRANSLATIONS[lang] && TRANSLATIONS[lang][key]) {
                if (el.tagName === 'SPAN') {
                    // For span elements (used in checkboxes/radios)
                    el.textContent = TRANSLATIONS[lang][key];
                } else if (el.tagName === 'OPTION') {
                    el.textContent = TRANSLATIONS[lang][key];
                } else if (el.tagName === 'TEXTAREA' || (el.tagName === 'INPUT' && el.type !== 'checkbox' && el.type !== 'radio')) {
                    el.placeholder = TRANSLATIONS[lang][key];
                } else if (el.tagName === 'BUTTON' && el.id) {
                    // 為按鈕更新文本，但保留emoji
                    const currentText = el.textContent.trim();
                    const emoji = currentText.match(/^[📋📊📝]/);
                    if (emoji) {
                        el.textContent = emoji[0] + ' ' + TRANSLATIONS[lang][key];
                    } else {
                        el.textContent = TRANSLATIONS[lang][key];
                    }
                } else if (el.tagName !== 'INPUT') {
                    el.textContent = TRANSLATIONS[lang][key];
                }
            }
        });

        // 更新動態消息文本
        updateDynamicTexts(lang);

        // 更新工具欄標題
        const barTitle = document.getElementById('bar-title');
        const bottomBar = document.getElementById('bottom-bar');
        if (barTitle && bottomBar) {
            if (bottomBar.classList.contains('collapsed')) {
                barTitle.textContent = TRANSLATIONS[lang]['toolsTitleShort'];
            } else {
                barTitle.textContent = TRANSLATIONS[lang]['toolsTitle'];
            }
        }

        // 1.5秒後自動收合語言切換器
        const langSwitcher = document.querySelector('.lang-switcher');
        if (langSwitcher) {
            clearTimeout(langSwitcherTimeout);
            langSwitcherTimeout = setTimeout(() => {
                langSwitcher.classList.remove('expanded');
            }, 1500);
        }

        // 保存語言偏好
        try {
            localStorage.setItem('preferredLang', lang); // eslint-disable-line no-restricted-globals
        } catch (e) {
            // localStorage 不可用時靜默失敗
        }
    }

    // 頁面靜置時自動收合語言切換器
    function resetPageIdleTimer() {
        const langSwitcher = document.querySelector('.lang-switcher');
        if (!langSwitcher) return;

        clearTimeout(pageIdleTimeout);
        pageIdleTimeout = setTimeout(() => {
            langSwitcher.classList.remove('expanded');
        }, 1500); // 1.5秒靜置後自動收合
    }

    // 滑動或其他活動時立即收合語言切換器
    function collapseLanguageSwitcher() {
        const langSwitcher = document.querySelector('.lang-switcher');
        if (langSwitcher && langSwitcher.classList.contains('expanded')) {
            langSwitcher.classList.remove('expanded');
        }
    }

    // 更新動態文本（消息框、確認按鈕等）
    function updateDynamicTexts(lang) {
        // 這個函數在生成消息時會被調用
        // 暫時保留為佔位符
    }

    // 頁面載入時恢復語言設置
    document.addEventListener('DOMContentLoaded', () => {
        try {
            const savedLang = localStorage.getItem('preferredLang'); // eslint-disable-line no-restricted-globals
            if (savedLang && TRANSLATIONS[savedLang]) {
                switchLanguage(savedLang);
            }
        } catch (e) {
            // localStorage 不可用时静默失败
        }

        // 语言切换器展开/收合功能
        const langSwitcher = document.querySelector('.lang-switcher');
        if (langSwitcher) {
            // 点击语言切换器展开
            langSwitcher.addEventListener('click', () => {
                langSwitcher.classList.add('expanded');
                clearTimeout(langSwitcherTimeout);
                clearTimeout(pageIdleTimeout);
            });

            // 点击其他位置收合
            document.addEventListener('click', (e) => {
                if (!langSwitcher.contains(e.target)) {
                    langSwitcher.classList.remove('expanded');
                }
            });
        }

        // 监听滚动和触摸移动时立即收合语言切换器
        ['scroll', 'touchmove'].forEach(eventType => {
            document.addEventListener(eventType, collapseLanguageSwitcher, { passive: true });
        });

        // 监听其他页面活动来重置静置计时器
        ['mousemove', 'keydown', 'click'].forEach(eventType => {
            document.addEventListener(eventType, resetPageIdleTimer, { passive: true });
        });

        // 初始启动静置计时器
        resetPageIdleTimer();
    });

    // --- 核心語料庫 (擴充版 - 包含單人讚美) ---
    const CORPUS = {
        en: {
            hype: [
                // CP向 & 人物（適用於藝人/角色，不適用於劇集）
                "{Input} are insaneeeee. I literally can't breathe right now ahhhhhhh",
                "My jaw dropped on the floor, {Input} served so hard today OMG",
                "How is {Input} even real? I'm losing my mind right now",
                "Sending all my love and support to {Input} su su na!",
                "Can we just appreciate {Input} for a moment? WOW.",
                "I'M SCREAMING SO LOUDDDDD {Input} IS EVERYTHING!!!!",
                "I love {Input} soooooo muchhhhh can't get enoughhhhhh",
                "I am a big fan of {Input} and always will be!",
                "Proud to be a fan of {Input}, they deserve all the love!",
                "Forever supporting {Input}, they mean the world to me!",
                "I am such a huge fan of {Input}, they never disappoint!",
                "Being a fan of {Input} is the best decision I ever made!",
                "We will always support {Input} no matter what happens!!!",
                "They are my sunshine and I love them so much {Input}",
                "{Input} are my angels sent from heaven I swear!!!",
                "How come {Input} can be THAT perfect it's unreal!!!",
                "{Input} owns my heart completely and utterly!!!",
                "Living for {Input} content every single day!!!",
                "My ultimate comfort and happiness is {Input}!!!",
                "Nothing makes me happier than seeing {Input}!!!",
                "{Input} brings so much joy into my life!!!",
                "Thank you {Input} for existing you're everything!!!",
                "My whole world revolves around {Input} honestly!!!",
                "I would do anything for {Input} no questions asked!!!",
                "No one does it like {Input} absolutely unmatched!!!",
                "The talent the visuals the everything {Input} has it ALL!!!",
                "{Input} deserves the entire universe and more!!!",
                "My biggest pride and joy is being a fan of {Input}!!!",
                "Can't imagine my life without {Input} anymore!!!",
                "{Input} makes everything better just by existing!!!",
                "Eternally grateful to have {Input} in my life!!!",
                // 單人讚美（只適用於人物）
                "{Input} is soooo handsome I can't even deal with it!!!",
                "How is {Input} THIS attractive it should be illegal omggg",
                "{Input} is the cutest baby ever I'm MELTING!!!",
                "My cute baby {Input} deserves all the love in the world!!!",
                "{Input} smile makes my whole day brighter ahhhhh",
                "I just can't breathe when {Input} smiles like that omggg",
                "{Input} is so precious and deserves the entire world!!!",
                "How come {Input} can be that handsome it's not fair!!!",
                "They are so cute I want to protect {Input} forever!!!",
                "He is so cute I'm gonna CRY {Input} is everything!!!",
                "He is so handsome {Input} takes my breath away!!!",
                "{Input} aura is just different from everyone else!!!",
                "The charisma {Input} has is absolutely insane!!!",
                "Everything {Input} does is so effortlessly cool!!!",
                "{Input} energy is unmatched nobody compares!!!",
                "The way {Input} carries himself is so attractive!!!",
                "Falling harder for {Input} every single day!!!",
                "{Input} has me in a chokehold and I'm not complaining!!!",
                "Obsessed doesn't even begin to describe how I feel about {Input}!!!",
                // 劇集/角色（可包含劇集名）
                "Handsome inspector {Input} is sooo attractive in this scene!!",
                "Captain {Input} riding a bike's just so COOL I'm screaming~",
                "Inspector {Input} solving cases is my new favorite thing to watch",
                "Captain {Input} in action scenes? PERFECTION!!!",
                "{Input} character arc is beautifully written I'm obsessed!!!",
                "The way {Input} portrayed this role is chef's kiss!!!",
                "{Input} is on the horizon",
                "{Input} is entering the timeline",
                "{Input} is waking up",
                "{Input} is getting closer",
                "{Input} is stepping into motion",
                "{Input} is loading its next phase",
                "{Input} is in progress",
                "{Input} is activating soon",
                "{Input} is preparing the moment",
                "{Input} is forming in the shadows",
                "{Input} is brewing quietly",
                "{Input} is lining up the pieces",
                "{Input} is powering up",
                "{Input} is ready to surface",
                "{Input} is stirring curiosity",
                "{Input} is approaching the scene",
                "{Input} is finding its rhythm",
                "{Input} is gathering attention",
                "{Input} is pulling focus",
                "{Input} is charged with energy",
                // 通用（適用於人物、CP、劇集）
                "ABSOLUTELY AMAZINGGGGGG!!! {Input} NEVER DISAPPOINTS!!!",
                "{Input} hits differentttttt every single timeeeeee",
                "No thoughts head empty just {Input} ahhhhhhhhhh",
                "THIS IS THE BEST THING EVER. I AM OBSESSED WITH {Input}",
                "CANNOT HANDLE THIS RIGHT NOWWWW {Input} TOO POWERFUL!!!",
                "YESSSSSS {Input} SLAYYYYYED SO HARDDDDDD!!!!",
                "OMG OMG OMG {Input} I'M LITERALLY SHAKINGGGGG!!!!",
                "This is soooooo gooddddd {Input} is perfectttttt",
                "Sooooo excitedddddd for {Input} ahhhhhhhhh",
                "{Input} is amazingggggg beyondddddd wordssssss",
                "I'm BEYOND EXCITED for {Input} this is unreal!!!",
                "Completely OVERWHELMED by {Input} in the best way possible!",
                "Can't wait can't wait CANNOT WAIT for {Input}!!!",
                "{Input} keeps getting better and better I'm SHOOK!!!",
                "The quality of {Input} is absolutely TOP TIER!!!",
                "Nobody is doing it like {Input} right now NOBODY!!!",
                "{Input} supremacy and that's on PERIOD!!!",
                "The hype for {Input} is so real and so deserved!!!",
                "{Input} era is the best era fight me on this!!!",
                "This {Input} content is feeding me so well!!!",
                "Bless whoever gave us {Input} seriously BLESS!!!",
                "{Input} never misses always delivers excellence!!!",
                "The standard is {Input} everyone else go home!!!",
                // 不需要Input的通用语句（適用於所有）
                "This is absolutely INSANE I'm literally screaming right now!!!",
                "OMG OMG OMG I can't handle this anymore!!!",
                "I'M SO EXCITEDDDDD THIS IS AMAZINGGGGGG!!!",
                "WOW WOW WOW this is EVERYTHING I needed today!!!",
                "This hits SO DIFFERENT I'm literally OBSESSED!!!",
                "YESSSSS THIS IS PERFECTTTTT SO SO GOOD!!!",
                "I'm screaming crying throwing up THIS IS TOO MUCH!!!",
                "Absolutely PHENOMENAL cannot get enough of this!!!",
                "This is PURE PERFECTION loving every second!!!",
                "SO SO GOOD I'm completely blown away right now!!!",
                "I just can't breathe right now this is too much!!!",
                "They are so cute together I'm literally melting!!!",
                "How come they can be that handsome it should be illegal!!!",
                "He is so precious and deserves everything!!!",
                "He is so handsome it takes my breath away!!!",
                "My heart is so full right now I could burst!!!",
                "This made my entire week no joke!!!",
                "I'm not okay I will NEVER be okay!!!",
                "The way I'm literally ASCENDING right now!!!",
                "This is everything I hoped for and MORE!!!",
                "I have no words just pure EMOTIONS!!!",
                "Crying happy tears this is beautiful!!!",
                "My serotonin levels are through the ROOF!!!",
                "This is the content I LIVE FOR!!!",
                "I'm floating on cloud nine right now!!!",
                "Best day ever thanks to this!!!",
                "Smiling so hard my face hurts!!!"
            ],
            chemistry: [
                // CP 向
                "The chemistry between {Input} is absolutely electric and undeniable",
                "Just look at the way {Input} look at each other, this is not acting",
                "{Input} have the most PERFECT chemistry I've ever seen!!!!",
                "Shipping {Input} HARDDDDD their connection is UNREAL!!!",
                "The way {Input} interact is sooooo natural I'm MELTING",
                "{Input} together is pure MAGIC no one can convince me otherwise",
                "Every {Input} moment has me SWOONING they're perfect together!!!",
                "This is not acting, {Input} is real and you can't tell me otherwise",
                "The tension in this scene? {Input} masterclass right there, my heart is racing",
                "My heart is fluttering so fast watching {Input}, they were made for each other",
                "The best partners in crime {Input}, love them so much forever and ever",
                "We need more {Input} moments, this is what keeps me alive",
                "{Input} chemistry is OFF THE CHARTS completely insane!!!",
                "Can we talk about {Input} chemistry? ABSOLUTELY FIERY!!!!",
                "{Input} looks at each other and I just LOSE IT every time",
                "The sparks between {Input} are FLYING I can feel it!!!",
                "I'm totally SOLD on {Input} their chemistry is everything!!!",
                "{Input} is the best, byebye ghostship 555555",
                // CP互动相关 - Eye Contact & Skinship
                "The EYE CONTACT between {Input} is INTENSE I'm blushing so hard!!!",
                "Did you see the way {Input} hold hands? My heart can't take this!!!",
                "{Input} clingy moments are the CUTEST THING EVER I'm screaming!!!",
                "The way {Input} always stay close to each other is so SWEET!!!",
                "{Input} looking at each other like THAT I'm not okay right now!!!",
                "Stop it {Input} the hand placement is TOO MUCH for my heart!!!",
                "I just realized {Input} positioning is so natural it fits perfectly",
                "{Input} possessive moments have me FEELING THINGS omggg!!!",
                "The way {Input} can't keep their hands off each other is everything!!!",
                "That moment when {Input} touched I literally STOPPED BREATHING!!!",
                "{Input} being this close together should be ILLEGAL my heart!!!",
                "Can we talk about {Input} body language? It's so INTIMATE!!!",
                "{Input} sweet moments together never end and I'm HERE FOR IT!!!",
                "The timing, the touch, everything about {Input} just CLICKS!!!",
                "{Input} jealous moments are low-key ADORABLE I can't handle it!!!"
            ],
            visuals: [
                // 通用
                "The visual explosion of {Input} in this set is truly insane and beautiful",
                "Can we talk about {Input}'s outfit? They look absolutely stunning today!",
                "Every single angle of {Input} is a masterpiece, a visual feast for the eyes",
                "Too much handsomeness/beauty in one frame from {Input}. I'm blessed",
                "{Input} served their best look yet, this comeback is epic.",
                "{Input} looks GORGEOUSSSSS today I'm literally BREATHLESS!!!",
                "THE VISUALS!!! {Input} is serving LOOKS left and right!!!!",
                "{Input} outfit today is PERFECTTTTTT chef's kiss!!!",
                "How does {Input} look THIS GOOD it should be illegal!!!!",
                "{Input} visual game is STRONGGGGGG absolutely stunning!!!",
                "I can't handle how beautiful {Input} looks right nowwwww",
                "{Input} is GLOWING today the prettiest ever no contest!!!",
                "Every outfit {Input} wears is ICONIC they never miss!!!!",
                "{Input} walked in and I forgot how to BREATHE so beautiful!!!"
            ],
            series: [
                // 劇集/角色
                "Give {Input} an award right now for this performance! I am so proud",
                "This episode of {Input} is a masterpiece, the storyline is incredible",
                "The storytelling in {Input} is NEXT LEVEL incredible writing!!!",
                "Every episode of {Input} gets BETTER AND BETTER loving it!!!",
                "I'm HOOKED on {Input} can't stop watching it's addictive!!!!",
                "{Input} plot keeps me on the EDGE OF MY SEAT constantly!!!",
                "The character development in {Input} is AMAZING so well done!!!",
                "Binge-watched {Input} and it was WORTH EVERY SECOND!!!!",
                "Can't get over this episode of {Input} absolutely BRILLIANT!!!",
                "The emotional delivery from {Input} gave me goosebumps, a truly unforgettable scene",
                "Every single expression from {Input} is on point. The series is so well done",
                "I am so proud of how far {Input} has come in their acting journey, amazing work",
                "{Input} acting is PHENOMENALLLLL absolutely award-worthy!!!",
                "This scene in {Input} had me CRYING it's too powerful!!!!",
                "{Input} performance is OUTSTANDING I'm beyond impressed!!!!",
                "{Input} is quiet tension",
                "{Input} is controlled fear",
                "{Input} is steady unease",
                "{Input} is calm before impact",
                "{Input} is silent danger",
                "{Input} is restrained chaos",
                "{Input} is low-burning suspense",
                "{Input} is held breath",
                "{Input} is slow dread",
                "{Input} is watchful stillness",
                "{Input} is measured risk",
                "{Input} is tension in balance",
                "{Input} is composed love",
                "{Input} is calm with teeth",
                "{Input} is pressure beneath",
                "{Input} is danger without noise",
                "{Input} is steady pulse",
                "{Input} is quiet countdown",
                "{Input} is anticipation sharpened",
                "{Input} is calm that cuts"
            ],
            ost: [
                "The new OST for {Input} is absolutely perfect, I've been listening on repeat!",
                "Just heard the {Input} theme song and WOW, it gave me chills all over",
                "The OST captures the essence of {Input} so perfectly, this is a masterpiece",
                "Can't stop streaming the {Input} soundtrack, it's THAT good!",
                "The music in {Input} elevates every scene, pure perfection!",
                "{Input} OST is on REPEATTTTT can't stop listening!!!",
                "The theme song for {Input} is PERFECTION gives me chills!!!",
                "{Input} soundtrack hits DIFFERENTTTTT so emotional!!!",
                "I'm OBSESSED with {Input} OST it's stuck in my head!!!",
                "Every song in {Input} is a MASTERPIECE loving the music!!!",
                "{Input} OST makes me CRY every single time so beautiful!!!",
                "The music in {Input} is INCREDIBLEEEE adds so much emotion!!!",
                "Can't get enough of {Input} soundtrack it's AMAZING!!!",
                "{Input} theme song is my new FAVORITE on repeat forever!!!"
            ],
            call_to_action: [
                "Everyone stream {Input} right now! Let's get those numbers up!",
                "We're SO close to hitting the milestone for {Input}! Keep streaming everyone!",
                "Don't forget to watch {Input} on Netflix! Let's show our support!",
                "{Input} is trending! Keep it going everyone, let's make some noise!",
                "Quick reminder to stream and share {Input}! Every view counts!",
                "Let's get {Input} to the top! Stream, like, and share everyone!",
                "We're ALMOST THERE!!! Keep streaming {Input} we can do this!!!",
                "Let's break records with {Input} STREAM STREAM STREAM!!!",
                "{Input} deserves ALL the love let's SUPPORT SUPPORT SUPPORT!!!",
                "Don't stop now!!! Keep {Input} TRENDING we're so close!!!",
                "PUSH PUSH PUSH for {Input} we need those numbers UP!!!",
                "Rally everyone!!! {Input} needs our SUPPORT right now!!!",
                "Let's make {Input} NUMBER ONE keep streaming fam!!!",
                "We can hit the goal for {Input} DON'T STOP STREAMING!!!",
                "Time to MOBILIZE for {Input} let's show our power!!!",
                "All hands on deck!!! Stream {Input} and spread the word!!!"
            ]
        },
        th: {
            hype: [
                // CP向 & 人物（適用於藝人/角色，不適用於劇集）
                "โอ้ยยยย {Input} ทำถึงมากกกกกก ไม่ไหวแล้วแม่ ahhhhhh",
                "กรี๊ดดดดดดด {Input} ดีงามพระรามแปดมากเวอร์ 55555555",
                "ช่วยด้วยยยย {Input} หล่อ/สวย ทำลา���ล้างมากกกกกก",
                "รัก {Input} เท่าจักรวาลลลลลลลลลลลลลลลล",
                "ชอบมากกกกก {Input} ทำได้ดีเสมอมาาาา",
                "จะซัพพอร์ต {Input} ตลอดไปไม่ว่าจะเกิดอะไร!!!",
                "{Input} คือดวงอาทิตย์ของฉัน รักมากกกก",
                "{Input} คือนางฟ้าที่ส่งมาจากสวรรค์เลย!!!",
                "ทำไม {Input} ถึงได้สมบูรณ์แบบ���นาดนี้!!!",
                "{Input} ครองใจฉันไปเลยยยย รักมากกกก!!!",
                "ดูคอนเทนต์ {Input} ทุกวันไม่มีเบื่อเลย!!!",
                "{Input} คือความสุขของฉันเลยยยย!!!",
                "ไม่มีอะไรทำให้มีความสุขเท่า {Input} เลย!!!",
                "{Input} มอบความสุขให้ฉันมากมาย!!!",
                "ขอบคุณ {Input} ที่มีอยู่ คุณคือทุกอย่าง!!!",
                "โลกของฉันหมุนรอบ {Input} จริงๆ!!!",
                "ทำอะไรก็ได้เพื่อ {Input} ไม่ต้องถามเลย!!!",
                "ไม่มีใครทำได้เหมือน {Input} เทพสุดๆ!!!",
                "ความสามารถ ลุค ทุกอย่าง {Input} มีครบ!!!",
                "{Input} สมควรได้รับจักรวาลทั้งใบ!!!",
                "ภูมิใจที่สุดที่เป็นแฟน {Input}!!!",
                "นึกชีวิตไม่ออกถ้าไม่มี {Input} แล้ว!!!",
                "{Input} ทำให้ทุกอย่างดีขึ้นแค่มีอยู่!!!",
                "ขอบคุณจักรวาลที่มี {Input} ในชีวิต!!!",
                // 單人讚美（只適用於人物）
                "{Input} หล่อมากกกกกก ตาแทบไม่กระพริบเลย!!!",
                "หล่อที่สุดดดดด {Input} ทำไมถึงได้หล่อขนาดนี้!!!",
                "{Input} น่ารักมากกกก narak mak จนใจละลาย!!!",
                "ลูกน้อยที่น่ารัก {Input} สมควรได้รับความรักทั้งหมด!!!",
                "รอยยิ้มของ {Input} ทำให้วันนี้สดใสมากกก",
                "หายใจไม่ออกเลยตอนที่ {Input} ยิ้มแบบนั้น!!!",
                "{Input} น่ารักมากกกก สมควรได้รับทุกอย่างในโลกใบนี้!!!",
                "ทำไม {Input} ถึงได้หล่อขนาดนี้ ไม่ยุติธรรมเลย!!!",
                "น่ารักมากอยากปกป้อง {Input} ตลอดไป!!!",
                "เขาน่ารักมากกกก จะร้องไห้แล้ว {Input} คือทุกอย่าง!!!",
                "เขาหล่อมากกกก {Input} ทำให้หายใจไม่ออก!!!",
                "ออร่าของ {Input} ต่างจากคนอื่นมากกกก!!!",
                "คา���ิสม่าของ {Input} แรงสุดๆ เหลือเชื่อ!!!",
                "ทุกอย่างที่ {Input} ทำดูเท่สุดๆ!!!",
                "พลังของ {Input} ไม่มีใครเทียบได้เลย!!!",
                "ท่าทางของ {Input} ดูน่าดึงดูดมากกกก!!!",
                "ตกหลุมรัก {Input} มากขึ้นทุกวัน!!!",
                "{Input} จับใจฉันไว้แน่นๆ ไม่บ่น!!!",
                "หลงใหลไม่พอจะอธิบายความรู้���ึกต่อ {Input}!!!",
                // 劇集/角色（可包含劇集名）
                "สารวัตรหล่อ {Input} น่าสนใจมากในซีนนี้!!",
                "กัปตัน {Input} ขี่มอเตอร์ไซค์เท่มากกกก~",
                "สารวัตร {Input} ไขคดีคือสิ่งที่ชอบดูมากที่สุด",
                "กัปตัน {Input} ในซีนแอ็คชั่น? สมบูรณ์แบบเลย!!!",
                "พัฒนาการของตัวละคร {Input} เขียนได้สวยมาก!!!",
                "การแสดง {Input} ในบทนี้ปังสุดๆ!!!",
                "{Input} กำลังจะมาแล้ว",
                "{Input} กำลังเข้าสู่ไทม์ไลน์",
                "{Input} กำลังตื่นขึ้นมา",
                "{Input} กำลังเข้าใกล้มากขึ้น",
                "{Input} กำลังเริ่มเคลื่อนไหว",
                "{Input} กำลังโหลดเฟสถัดไป",
                "{Input} กำลังดำเนินการอยู่",
                "{Input} จะเปิดตัวเร็วๆ นี้",
                "{Input} กำลังเตรียมช่วงเวลาพิเศษ",
                "{Input} กำลังก่อตัวในเงามืด",
                "{Input} กำลังค่อยๆ เคลื่อนไหว",
                "{Input} กำลังเรียงชิ้นส่วน",
                "{Input} กำลังชาร์จพลัง",
                "{Input} พร้อมที่จะปรากฏตัว",
                "{Input} กำลังกระตุ้นความอยากรู้",
                "{Input} กำลังเข้าใกล้ฉาก",
                "{Input} กำลังหาจังหวะ",
                "{Input} กำลังดึงดูดความสนใจ",
                "{Input} กำลังดึงโฟกัส",
                "{Input} เต็มไปด้วยพลังงาน",
                // 通用（適用於人物、CP、劇集）
                "{Input} สุดยอดจริงๆ ภูมิใจมากกกกกก!!!",
                "ตายสงบศพสีชมพูเพราะ {Input} เลยวันนี้ ฮืออออออ",
                "{Input} คือที่สุดของที่สุด ไม่มีใครต้านได้แล้ว",
                "เขินจนตัวบิดไปหมดแล้วกับ {Input} งื้ออออออออออ",
                "ใครไหวไปก่อนเลย ทางนี้ไม่ไหวกับ {Input} แล้ว",
                "ขอยาดมด่วนนนน {Input} แรงมากกกกกกกก",
                "{Input} ดีมากกกก ตื่นเต้นจนนอนไม่หลับเลย!!!",
                "ตื่นเต้นมากกกกกก {Input} ทำให้ใจเต้นแรงงงงง",
                "เร้าใจสุดๆ กับ {Input} รอไม่ไหวแล้วววว",
                "ประทับใจมากกกก {Input} ยอดเยี่ยมที่สุดดดด",
                "{Input} ทำให้หัวใจเต้นแรงงง รู้สึกตื่นเต้นมาก!!!",
                "ฟินสุดๆๆๆ กับ {Input} ไม่มีคำไหนจะบรรยาย",
                "เกินคาดหมายยยย {Input} ดีกว่าที่คิดไว้อีก!!!",
                "ไม่มีคำไหนอธิบายได้นอกจาก {Input} สุดยอด!!!",
                "{Input} ดีขึ้นเรื่อยๆ ตกใจสุดๆ!!!",
                "คุณภาพของ {Input} ระดับท็อปเทียร์เลย!!!",
                "ไม่มีใครทำได้เหมือน {Input} ตอนนี้ ไม่มีเลย!!!",
                "{Input} เป็นใหญ่ จบข้อความ!!!",
                "การฮือฮาของ {Input} สมเหตุสมผลมากกกก!!!",
                "ยุค {Input} คือยุคที่ดีที่สุด เถียงไม่ได้!!!",
                "คอนเทนต์ {Input} เลี้ยงดูฉันได้อิ่มมาก!!!",
                "ขอบคุณคนที่มอบ {Input} ให้เรา จริงๆ!!!",
                "{Input} ไม่เคยพลาด ส่งมอบความเยี่ยมเสมอ!!!",
                "มาตรฐานคือ {Input} คนอื่นกลับบ้านได้แล้ว!!!",
                // 不需要Input的通用语句（適用於所有）
                "โอ้ยยยยย สุดยอดมากกกกกก ไม่ไหวแล้ววว!!!",
                "กรี๊ดดดดดด ดีงามมากเวอร์ 55555555",
                "ตื่นเต้นจนนอนไม่หลับเลยยยย สุดยอดดดดด!!!",
                "ฟินมากกกก ชอบสุดๆๆๆ เลยยยย!!!",
                "เกินห้ามใจมากกกก ประทับใจสุดๆ!!!",
                "ขอยาดมด่วนนนน แรงมากกกก 555555!!!",
                "เร้าใจสุดๆ รอไม่ไหวแล้วววว!!!",
                "หายใจไม่ออกเลยตอนนี้ มากเกินไป!!!",
                "น่ารักมากกกก อยู่ด้วยกันแล้วใจละลาย!!!",
                "ทำไมถึงได้หล่อขนาดนี้ ไม่ยุติธรรมเลย!!!",
                "เขาน่ารักมากกกก สมควรได้รับทุกอย่าง!!!",
                "เขาหล่อมากกกก ทำให้หายใจไม่ออก!!!",
                "หัวใจเต็มเปี่ยมมากกก จะระเบิดแล้ว!!!",
                "ทำให้อาทิตย์นี้สมบูรณ์เลย ไม่มีตลก!!!",
                "ไม่โอเค ไม่มีทางโอเคได้อีกแล้ว!!!",
                "กำลังลอยสู่สวรรค์อยู���ตอนนี้เลย!!!",
                "นี่คือทุกอย่างที่หวังและมากกว่า!!!",
                "ไม่มีคำพูดเหลือ มีแต่ความรู้สึก!!!",
                "ร้องไห้น้ำตาดีใจ สวยงามมาก!!!",
                "ระดับเซโรโทนินพุ่งทะลุหลังคา!!!",
                "นี่คือคอนเทนต์ที่ฉันมีชีวิตเพื่อ!!!",
                "ลอยอยู่บนเมฆาชั้นเก้าเลย!!!",
                "วันที่ดีที่สุดเลยขอบคุณนะ!!!",
                "ยิ้มจนหน้าเจ็บเลยยยย!!!"
            ],
            chemistry: [
                // CP 向
                "เคมีเคใจของ {Input} มันฟุ้งกระจายไปหมดดดดดดด",
                "สายตาที่ {Input} มองกันมันมีความหมายซ่อนอยู่ 555555555",
                "{Input} เคมีกันดีมากกกก ลงตัวที่สุดดด!!!",
                "ธรรมชาติมากกกก {Input} อยู่ด้วยกันแล้วโลกสดใส",
                "นี่มันคู่สร้างคู่สมชัดๆ {Input} เหมาะสมกันที่สุด",
                "ชิปเปอร์ตายเกลื่อนเพราะโมเมนต์ {Input} วันนี้ ahhhhhhh",
                "{Input} เรียลกว่านี้ไม่มีอีกแล้ว ฟินระดับสิบ",
                "คู่นี้ปังมากกก {Input} ความหวานล้นจอออ",
                "{Input} มองกันแบบนี้ ใจฉันจะวายยยย",
                "เกิดมาเพื่อกันชัดๆ {Input} คือคู่แท้!!!",
                "{Input} ใกล้กันทีไร หัวใจเต้นแรงงงง",
                "ชิปจมไปแล้ว {Input} เคมีดีเกินห้ามใจ!!!",
                "คู่จิ้นระดับโลก {Input} น่ารักมากกกกก",
                "{Input} คือพลังรักแท้ ไม่มีใครเทียบ!!!",
                "เห็น {Input} ด้วยกันแล้วอบอุ่นใจมาก",
                "{Input} คือที่สุด ลาก่อนเรือผี 555555",
                // CP互動相關 - Eye Contact & Skinship
                "สบตากันของ {Input} มันแรงมากกกก หน้าแดงไปหมดแล้ว!!!",
                "เห็น {Input} จับมือกันยัง ไม่ไหวแล้วหัวใจจะวาย!!!",
                "{Input} clingy moments น่ารักที่สุดเลย กรี๊ดดดดด!!!",
                "{Input} ติดกันตลอดเวลาน่ารักมากกกก ฟินสุดๆ!!!",
                "{Input} มองกันแบบนี้ ทนไม่ไหวแล้วจริงๆ!!!",
                "หยุดนะ {Input} วางมือแบบนี้หัวใจไม่ไหวแล้ว!!!",
                "เพิ่งสังเกต {Input} positioning ธรรมชาติมาก ลงตัวสุดๆ",
                "{Input} possessive moments ทำให้รู้สึกอะไรบางอย่าง!!!",
                "{Input} อยู่ใกล้กันตลอด ไม่อยากให้ห่างกันเลย!!!",
                "ช่วงที่ {Input} แตะกัน หยุดหายใจไปเลยจริงๆ!!!",
                "{Input} อยู่ใกล้กันแบบนี้ผิดกฎหมายแล้วนะ หัวใจไม่ไหว!!!",
                "ภาษากายของ {Input} มันใกล้ชิดมากกกก ฟินสุดๆ!!!",
                "{Input} โมเมนต์หวานๆ ไม่เคยจบเลย ชอบมากกกก!!!",
                "ทั้งจังหวะ การสัมผัส ทุกอย่างของ {Input} ลงตัวมาก!!!",
                "{Input} jealous moments น่ารักลับๆ อยู่เลย ฟินเว่อร์!!!"
            ],
            visuals: [
                "วิชวล {Input} วันนี้คือที่สุดของที่สุด หล่อ/สวย จนใจเจ็บ",
                "ชุดนี้ของ {Input} มันดีมากนะ แม่ขาาาaaaา 5555555",
                "หันมุมไหนก็หล่อ/สวยไปหมดเลย {Input} ดีเกินต้าน",
                "เกินไปมาก! {Input} ทำไมถึงได้ดูดีขนาดนี้คะ ฮืออออ",
                "ชอบลุคนี้ของ {Input} มากๆ ขอสิบเต็มสิบเลย",
                "{Input} สวย/หล่อจนแทบหยุดหายใจ สมบูรณ์แบบมาก!!!",
                "วิชวลระดับเทพ {Input} ดูดีทุกองศาาาา",
                "{Input} ลุคนี้ปังสุดๆ แต่งตัวเก่งมาก!!!",
                "หล่อ/สวยเกินห้ามใจ {Input} คือความสมบูรณ์แบบ!!!",
                "{Input} สวย/หล่อจนต้องจิ้มหน้าจอ ชอบมากกกก",
                "ดูดีทุกมุมมอง {Input} วิชวลเทพมากกกก",
                "{Input} แต่งตัวดีมาก สไตล์เจ๋งสุดๆ!!!",
                "ลุคนี้ของ {Input} ปังปุริเย่มาก หล่อ/สวยสุดๆ",
                "{Input} เปล่งประกายมาก ดูดีทุกครั้งเลย!!!"
            ],
            series: [
                "ซีนอารมณ์ {Input} ทำได้ดีมาก น้ำตาไหลตามเลย 555",
                "เนื้อเรื่อง {Input} เขียนได้ดีมาก ติดตามทุกตอน!!!",
                "ทุกตอนของ {Input} ดีขึ้นเรื่อยๆ ชอบมากกก",
                "ดู {Input} แล้วติดใจ ดูซ้ำไม่เบื่อเลย!!!",
                "พล็อต {Input} น่าติดตามมาก ลุ้นทุกตอนเลย",
                "ตัวละครใน {Input} พัฒนาดีมาก เขียนได้เจ๋ง!!!",
                "ดู {Input} จบรอบแล้ว คุ้มค่าทุกนาทีเลย",
                "ตอนนี้ของ {Input} ยอดเยี่ยมมาก ประทับใจสุดๆ",
                "การแสดงของ {Input} พัฒนาไปไกลมาก ภูมิใจสุดๆ",
                "ขนลุกไปหมดแล้ว {Input} เล่นด���จนต้องกราบ",
                "บทบาทนี้เกิดมาเพื่อ {Input} จริงๆ ยอมรับเลย",
                "{Input} ไม่เคยทำให้ผิดหวังเลยจริงๆ เก่งมาก!",
                "{Input} แสดงดีมากกกก ควรได้รางวัลเลย!!!",
                "ซีนนี้ใน {Input} ทำให้น้ำตาไหล ซึ้งมากกก",
                "{Input} การแสดงระดับเทพ ประทับใจสุดๆ",
                "{Input} คือความตึง���ครียดที่เงียบ",
                "{Input} คือความกลัวที่ควบคุมได้",
                "{Input} คือความไม่สบายใจที่คงที่",
                "{Input} คือความสงบก่อนพายุ",
                "{Input} คืออันตรายที่เงียบงัน",
                "{Input} คือความโกลาหลที่ถูกกดไว้",
                "{Input} คือความระทึกที่ค่อยๆ ลุกไหม้",
                "{Input} คือลมหายใจที่กลั้นไว้",
                "{Input} คือความหวาดกลัวที่ช้าๆ",
                "{Input} คือความนิ่งที่เฝ้าดู",
                "{Input} คือความเสี่ยงที่วัดได้",
                "{Input} คือความตึงเครียดที่สมดุล",
                "{Input} คือความรักที่สงบ",
                "{Input} คือความสงบที่มีเขี้ยว",
                "{Input} คือแรงกดดันที่ซ่อนอยู่",
                "{Input} คืออันตรายไร้เสียง",
                "{Input} คือจังหวะที่คงที่",
                "{Input} คือการนับถอยหลังที่เงียบ",
                "{Input} คือความคาดหวังที่คมกริบ",
                "{Input} คือความสงบที่ตัดเฉือน"
            ],
            ost: [
                "เพลงประกอบ {Input} ฟังเพราะมากกกก ฟังซ้ำไปซ้ำมาเลย",
                "OST ของ {Input} โดนใจสุดๆ ขนลุกทุกครั้งที่ได้ฟัง",
                "เพลงใน {Input} เข้ากับบรรยากาศมากเกินไป ชอบมากกก",
                "ทำไม OST {Input} ถึงได้ดีขนาดนี้ ฟังไม่เบื่อเลย!",
                "เพลงประกอบของ {Input} ยกระดับซีรีส์ขึ้นไปอีก สุดยอด!",
                "{Input} OST ฟังซ้ำไม่รู้กี่รอบ ติดหูมากกกก",
                "เพลงประกอบ {Input} เพราะจนต้องร้องไห้ ซึ้งมาก!!!",
                "{Input} soundtrack เพราะทุกเพลงเลย ชอบสุดๆ",
                "ติดหู {Input} OST มากกกก ฟังไปร้องไปเลย!!!",
                "ทุกเพลงใน {Input} คือผลงานชิ้นเอก เพราะมาก",
                "{Input} OST ทำให้น้ำตาไหล ซาวด์แทร็กดีมาก!!!",
                "���นตรีใน {Input} เพิ่มอารมณ์มากกกก เพราะสุดๆ",
                "เพลง {Input} ฟังไม่พอ เพราะเกินห้ามใจ!!!",
                "{Input} theme song คือเพลงโปรดใหม่ ฟังตลอด"
            ],
            call_to_action: [
                "ทุกคนช่วยกันสตรีม {Input} ด้วยนะคะ ต้องการกำลังใจ!",
                "เกือบถึงเป้าแล้วสำหรับ {Input} ช่วยกันสตรีมต่อ!",
                "อย่าลืมไปดู {Input} ใน Netflix กันนะ ช่วยกันซัพพอร์ต!",
                "{Input} กำลังเทรนด์! ช่วยกันปั่นต่อไปเลย!",
                "เตือนความจำว่าต้องสตรีมและแชร์ {Input} กันนะ!",
                "ช่วยกันพา {Input} ขึ้นอันดับกันเถอะ สตรีม กด like และแชร์!",
                "เกือบถึงแล้ว!!! ช่วยกันสตรีม {Input} ต่อไปเลย",
                "มาทำสถิติกับ {Input} กันเถอะ สตรีม สตรีม สตรีม!!!",
                "{Input} สมควรได้รับความรัก ช่วยกันซัพพอร์ตตต",
                "อย่าหยุด!!! ช่วยให้ {Input} เทรนด์ต่อไป เกือบแล้ว",
                "ปั่น ปั่น ปั่นนน {Input} ต้องการตัวเลขเพิ่ม!!!",
                "ระดมกันเลย!!! {Input} ต้องการซัพพอร์ตตอนนี้",
                "ทำให้ {Input} ขึ้นอันดับ 1 กันเถอะ สตรีมต่อ!!!",
                "เราทำเป้าหมายให้ {Input} ได้ อย่าหยุดสตรีมนะ",
                "ถึงเวลาระดมพลสำหรับ {Input} แล้ว มาช่วยกัน!!!",
                "ทุกคนช่วยกัน!!! สตรีม {Input} แล้วบอกต่อด้วย"
            ]
        }
    };

    const EMOJIS = ["✨", "💖", "🔥", "🤩", "😭", "🤯", "😍", "💫", "🥹", "❤️‍🔥", "⚡️", "👑", "👍", "💯", "🥺", "🌟", "💕", "😱", "🙌", "💗"];
    const NEGATIVE_WORDS = ['die', 'hate', 'stupid', 'bad', 'ugly', 'worst', '垃圾', '爛', '差', '討厭', '噁心', '去死'];

    // --- Toggle 功能：添加或移除文字 ---
    function toggleTextInField(fieldId, text) {
        const field = document.getElementById(fieldId);
        if (!field) return;

        const currentValue = field.value.trim();

        if (fieldId === 'mandatory-text') {
            // 必須字句框：簡單的空格分隔
            const parts = currentValue.split(/\s+/).filter(p => p.length > 0);
            const index = parts.indexOf(text);

            if (index >= 0) {
                // 已存在，移除
                parts.splice(index, 1);
                field.value = parts.join(' ');
            } else {
                // 不存在，添加
                if (!currentValue) {
                    field.value = text;
                } else {
                    field.value = currentValue + ' ' + text;
                }
            }
        } else if (fieldId === 'free-text') {
            // 自由描述框：逗號分隔
            const parts = currentValue.split(/[,，]/).map(s => s.trim()).filter(s => s.length > 0);
            const index = parts.indexOf(text);

            if (index >= 0) {
                // 已存在，移除
                parts.splice(index, 1);
                field.value = parts.join(', ');
            } else {
                // 不存在，添加
                if (parts.length === 0) {
                    field.value = text;
                } else {
                    field.value = parts.join(', ') + ', ' + text;
                }
            }
        }
    }

    // --- 自定義 Modal 函數 ---
    function showMessage(message) {
        const modal = document.createElement('div');
        modal.className = 'custom-modal';
        const confirmText = TRANSLATIONS[currentLang]['confirm'];
        modal.innerHTML = `
            <div class="custom-modal-content">
                <p>${message}</p>
                <button onclick="this.closest('.custom-modal').remove()">${confirmText}</button>
            </div>
        `;
        document.body.appendChild(modal);
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                modal.remove();
            }
        });
    }

    // --- 自定義確認對話框 ---
    function showConfirm(message, onConfirm) {
        const modal = document.createElement('div');
        modal.className = 'custom-modal';
        modal.innerHTML = `
            <div class="custom-modal-content">
                <p>${message}</p>
                <div style="display: flex; gap: 12px; margin-top: 20px;">
                    <button onclick="this.closest('.custom-modal').remove()" style="flex: 1; background: var(--card-bg); color: var(--text-primary); box-shadow: 4px 4px 8px var(--shadow-dark), -4px -4px 8px var(--shadow-light);">取消</button>
                    <button id="confirm-yes-btn" style="flex: 1;">確定</button>
                </div>
            </div>
        `;
        document.body.appendChild(modal);

        const yesBtn = modal.querySelector('#confirm-yes-btn');
        yesBtn.addEventListener('click', () => {
            modal.remove();
            onConfirm();
        });

        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                modal.remove();
            }
        });
    }

    // --- 直接滾動到結果 ---
    function showScrollHint() {
        // 直接滾動到結果區域，不需要倒計時
        scrollToResultsSection();
    }

    function scrollToResultsSection() {
        const resultsTitle = document.getElementById('results-title');
        if (resultsTitle) {
            resultsTitle.scrollIntoView({
                behavior: 'smooth',
                block: 'start'
            });
        }
    }

    // --- 切換底部操作欄 ---
    function toggleActionBar() {
        const bar = document.getElementById('bottom-bar');
        const icon = document.getElementById('toggle-icon');
        const title = document.getElementById('bar-title');

        if (!bar || !icon || !title) return;

        if (bar.classList.contains('expanded')) {
            bar.classList.remove('expanded');
            bar.classList.add('collapsed');
            icon.textContent = '▲';
            title.textContent = TRANSLATIONS[currentLang]['toolsTitleShort'];
        } else {
            bar.classList.remove('collapsed');
            bar.classList.add('expanded');
            icon.textContent = '▼';
            title.textContent = TRANSLATIONS[currentLang]['toolsTitle'];
        }
    }

    // --- 可拖放按鈕功能 ---
    let isDragging = false;
    let currentX;
    let currentY;
    let initialX;
    let initialY;
    let xOffset = 0;
    let yOffset = 0;
    let lastClickTime = 0;
    const DOUBLE_CLICK_DELAY = 300; // 300ms 內的兩次點擊視為雙擊

    function dragStart(e) {
        const backToTopBtn = document.getElementById('back-to-top');
        if (!backToTopBtn) return;

        if (e.type === "touchstart") {
            initialX = e.touches[0].clientX - xOffset;
            initialY = e.touches[0].clientY - yOffset;
        } else {
            initialX = e.clientX - xOffset;
            initialY = e.clientY - yOffset;
        }

        if (e.target === backToTopBtn) {
            isDragging = true;
            backToTopBtn.classList.add('dragging');
        }
    }

    function dragEnd(e) {
        const backToTopBtn = document.getElementById('back-to-top');
        if (!backToTopBtn) return;

        if (isDragging) {
            initialX = currentX;
            initialY = currentY;
            isDragging = false;
            backToTopBtn.classList.remove('dragging');

            // 保存位置到 localStorage
            try {
                localStorage.setItem('backToTopX', xOffset); // eslint-disable-line no-restricted-globals
                localStorage.setItem('backToTopY', yOffset); // eslint-disable-line no-restricted-globals
            } catch (e) {
                // localStorage 不可用時靜默失敗
            }
        }
    }

    function drag(e) {
        const backToTopBtn = document.getElementById('back-to-top');
        if (!backToTopBtn) return;

        if (isDragging) {
            e.preventDefault();

            let newX, newY;
            if (e.type === "touchmove") {
                newX = e.touches[0].clientX - initialX;
                newY = e.touches[0].clientY - initialY;
            } else {
                newX = e.clientX - initialX;
                newY = e.clientY - initialY;
            }

            // 獲取按鈕尺寸和視窗尺寸
            const btnWidth = 55; // 固定按钮宽度
            const btnHeight = 55; // 固定按钮高度

            // 計算邊界限制 (确保按钮至少有一半在可见范围内)
            const minX = -btnWidth / 2;
            const maxX = window.innerWidth - btnWidth / 2;
            const minY = -btnHeight / 2;
            const maxY = window.innerHeight - btnHeight / 2;

            // 限制在邊界內
            currentX = Math.max(minX, Math.min(maxX, newX));
            currentY = Math.max(minY, Math.min(maxY, newY));

            xOffset = currentX;
            yOffset = currentY;

            // 使用 requestAnimationFrame 提升流暢度
            requestAnimationFrame(() => {
                setTranslate(currentX, currentY, backToTopBtn);
            });
        }
    }

    function setTranslate(xPos, yPos, el) {
        if (el) {
            el.style.transform = `translate3d(${xPos}px, ${yPos}px, 0)`;
        }
    }

    function scrollToResults() {
        if (!isDragging) {
            const currentTime = new Date().getTime();
            const timeDiff = currentTime - lastClickTime;

            // 檢測雙擊
            if (timeDiff < DOUBLE_CLICK_DELAY && timeDiff > 0) {
                // 雙擊：回到最頂部
                window.scrollTo({
                    top: 0,
                    behavior: 'smooth'
                });
                lastClickTime = 0; // 重置點擊時間
            } else {
                // 單擊：回到生成結果
                scrollToResultsSection();
                lastClickTime = currentTime;
            }
        }
    }

    // --- 輔助函數 ---
    function getRandomItem(arr) {
        if (!arr || arr.length === 0) return null;
        return arr[Math.floor(Math.random() * arr.length)];
    }

    function containsThai(text) {
        return /[\u0E00-\u0E7F]/.test(text);
    }

    // 將自由描述拆分成詞彙數組
    function parseFreeTextInputs(freeText) {
        if (!freeText) return [];
        return freeText.split(/[,，]/).map(s => s.trim()).filter(s => s.length > 0);
    }

    // 根據目標語言選擇合適的輸入詞
    function selectAppropriateInput(inputArray, targetLang) {
        if (!inputArray || inputArray.length === 0) return null;

        // 過濾掉不合適的詞（例如英文推文不使用泰文詞）
        const suitableInputs = inputArray.filter(input => {
            if (targetLang === 'en' && containsThai(input)) {
                return false;
            }
            return true;
        });

        if (suitableInputs.length === 0) return null;
        return getRandomItem(suitableInputs);
    }

    function replaceInput(template, selectedInput) {
        if (!selectedInput) {
            return null; // 返回 null 表示這個模板不應該使用
        }
        return template.replace(/\{Input\}/g, selectedInput);
    }

    function isNegative(text) {
        if (!text) return false;
        const lowerText = text.toLowerCase();
        return NEGATIVE_WORDS.some(word => lowerText.includes(word));
    }

    // --- 主要生成邏輯 ---
    function generateTweets() {
        const mandatoryText = document.getElementById('mandatory-text').value.trim();
        const freeText = document.getElementById('free-text').value.trim();
        const position = document.querySelector('input[name="position"]:checked').value;
        const lang = document.getElementById('output-lang').value;
        const includeEmoji = document.getElementById('include-emoji').checked;
        const quantity = parseInt(document.getElementById('selected-qty').value);
        const selectedThemes = Array.from(document.querySelectorAll('input[name="theme"]:checked')).map(cb => cb.value);

        const tweetsList = document.getElementById('tweets-list');
        const resultsContainer = document.getElementById('results-container');
        const bottomBar = document.getElementById('bottom-bar');
        const statusDisplay = document.getElementById('generation-status');
        tweetsList.innerHTML = '';

        if (selectedThemes.length === 0) {
            showMessage(TRANSLATIONS[currentLang]['msgSelectTheme']);
            return;
        }

        if (isNegative(freeText)) {
            showMessage(TRANSLATIONS[currentLang]['msgNegativeWords']);
            return;
        }

        let fullCorpus = [];
        if (lang === 'mix') {
            selectedThemes.forEach(theme => {
                fullCorpus.push(...(CORPUS.en[theme] || []).map(t => ({text: t, lang: 'en'})));
                fullCorpus.push(...(CORPUS.th[theme] || []).map(t => ({text: t, lang: 'th'})));
            });
        } else {
            selectedThemes.forEach(theme => {
                fullCorpus.push(...(CORPUS[lang][theme] || []).map(t => ({text: t, lang: lang})));
            });
        }

        if (fullCorpus.length === 0) {
            showMessage(TRANSLATIONS[currentLang]['msgNoCorpus']);
            return;
        }

        // 解析自由描述為詞彙數組
        const inputArray = parseFreeTextInputs(freeText);

        const generatedTweets = new Set();
        let attempts = 0;
        const maxAttempts = quantity * 10;

        while (generatedTweets.size < quantity && attempts < maxAttempts) {
            attempts++;

            const corpusItem = getRandomItem(fullCorpus);
            const rawSentence = corpusItem.text;
            const currentLang = corpusItem.lang;

            // 隨機選擇一個合適的輸入詞
            const selectedInput = selectAppropriateInput(inputArray, currentLang);

            // 如果模板需要{Input}但沒有合適的詞，跳過這個模板
            if (rawSentence.includes('{Input}') && !selectedInput) {
                continue;
            }

            // 替換模板中的 {Input}
            let sentence = selectedInput ? rawSentence.replace(/\{Input\}/g, selectedInput) : rawSentence;

            if (sentence.length <= 15) {
                const fillers = currentLang === 'en' ? [' ahhhhhhh', ' soooooooooo good', ' OMGOMGOMG'] : [' 55555555555', ' ฮืออออออออออ', ' สุดยอดดดดด'];
                sentence += getRandomItem(fillers);
            }

            if (includeEmoji) {
                sentence += ' ' + getRandomItem(EMOJIS);
            }

            let finalTweet = '';
            const separator = '\n\n';

            if (position === 'prefix' && mandatoryText) {
                finalTweet = `${mandatoryText}${separator}${sentence}`;
            } else if (position === 'suffix' && mandatoryText) {
                finalTweet = `${sentence}${separator}${mandatoryText}`;
            } else {
                finalTweet = sentence;
            }

            if (!generatedTweets.has(finalTweet.trim())) {
                generatedTweets.add(finalTweet.trim());
                renderTweet(finalTweet);
            }
        }

        resultsContainer.style.display = 'block';
        bottomBar.style.display = 'block';
        statusDisplay.textContent = TRANSLATIONS[currentLang]['msgGenSuccess'].replace('{count}', generatedTweets.size);

        // 初始化選擇計數
        updateSelectionCount();

        showScrollHint();
    }

    // --- 渲染結果到介面 ---
    function renderTweet(content) {
        const tweetsList = document.getElementById('tweets-list');
        const item = document.createElement('div');
        item.className = 'result-item';
        item.dataset.content = content;

        // 移除內容前後的空格並替換換行符
        const cleanContent = content.trim().replace(/\n/g, '<br>');

        item.innerHTML = `
            <input type="checkbox" class="tweet-checkbox" checked>
            <div class="result-text">${cleanContent}</div>
            <div class="result-actions">
                <button class="post-to-x-btn">
                    ✈️
                </button>
            </div>
        `;

        // 使用事件監聽器而不是內聯onclick，避免特殊字符問題
        const postBtn = item.querySelector('.post-to-x-btn');
        postBtn.addEventListener('click', (e) => {
            e.preventDefault();
            e.stopPropagation();
            postToX(content);
        });

        tweetsList.appendChild(item);
    }

    // --- X.com 分享連結 ---
    function postToX(text) {
        try {
            // 確保文本被正確編碼
            const encodedText = encodeURIComponent(text);
            const url = `https://twitter.com/intent/tweet?text=${encodedText}`;

            // 嘗試打開新窗口
            const newWindow = window.open(url, '_blank');

            // 檢測是否成功打開
            if (!newWindow || newWindow.closed || typeof newWindow.closed === 'undefined') {
                // 彈窗被阻止，提供備用方案
                showMessage('❌ 彈窗被瀏覽器阻止。請允許彈窗或手動複製鏈接。');
            }
        } catch (err) {
            console.error('發送到X失敗:', err);
            showMessage('❌ 發送失敗，請稍後再試。');
        }
    }

    // --- Excel 導出功能 ---
    function exportToExcel() {
        const checkedItems = Array.from(document.querySelectorAll('.tweet-checkbox:checked'));
        if (checkedItems.length === 0) {
            showMessage(TRANSLATIONS[currentLang]['msgSelectTweets']);
            return;
        }

        let csvContent = "data:text/csv;charset=utf-8,\uFEFF";
        csvContent += "序號,內容\n";

        checkedItems.forEach((checkbox, index) => {
            const content = checkbox.closest('.result-item').dataset.content;
            // 保留換行符以便在 Excel 中顯示為多行
            const cleanContent = `"${content.replace(/"/g, '""')}"`;
            csvContent += `${index + 1},${cleanContent}\n`;
        });

        const encodedUri = encodeURI(csvContent);
        const link = document.createElement("a");
        link.setAttribute("href", encodedUri);
        link.setAttribute("download", "Twitter_Posts_Export.csv");
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        showMessage(TRANSLATIONS[currentLang]['msgExportSuccess'].replace('{count}', checkedItems.length));
    }

    // --- 純文本導出功能 ---
    function exportToText() {
        const checkedItems = Array.from(document.querySelectorAll('.tweet-checkbox:checked'));
        if (checkedItems.length === 0) {
            showMessage(TRANSLATIONS[currentLang]['msgSelectTweets']);
            return;
        }

        const timestamp = new Date().toLocaleString('zh-TW');
        let textContent = `推文導出\n生成時間：${timestamp}\n${'='.repeat(50)}\n\n`;

        checkedItems.forEach((checkbox, index) => {
            const content = checkbox.closest('.result-item').dataset.content;
            textContent += `推文 #${index + 1}\n${'-'.repeat(50)}\n${content}\n\n`;
        });

        textContent += `${'='.repeat(50)}\n共 ${checkedItems.length} 則推文 | 由 FC刷推生成器 生成`;

        const blob = new Blob([textContent], { type: 'text/plain;charset=utf-8' });
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.setAttribute('href', url);
        link.setAttribute('download', 'Twitter_Posts_Export.txt');
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
        URL.revokeObjectURL(url);
        showMessage(TRANSLATIONS[currentLang]['msgExportTxtSuccess'].replace('{count}', checkedItems.length));
    }

    // --- 事件監聽器 ---
    document.addEventListener('DOMContentLoaded', () => {
        // 恢復主題偏好
        try {
            const savedTheme = localStorage.getItem('preferredTheme'); // eslint-disable-line no-restricted-globals
            if (savedTheme) {
                switchTheme(savedTheme);
            }
        } catch (e) {
            // localStorage 不可用时静默失败
        }

        // 檢查是否需要顯示教學
        try {
            const hideTutorial = localStorage.getItem('hideTutorial'); // eslint-disable-line no-restricted-globals
            if (!hideTutorial) {
                // 延遲1秒後顯示教學，讓頁面先加載完成
                setTimeout(showTutorial, 1000);
            }
        } catch (e) {
            // localStorage 不可用时显示教学
            setTimeout(showTutorial, 1000);
        }

        // 數量選擇
        const quantityOptions = document.getElementById('quantity-options');
        if (quantityOptions) {
            quantityOptions.addEventListener('click', (e) => {
                if (e.target.tagName === 'BUTTON') {
                    document.querySelectorAll('#quantity-options button').forEach(btn => btn.classList.remove('active'));
                    e.target.classList.add('active');
                    document.getElementById('selected-qty').value = e.target.dataset.qty;
                }
            });
        }

        // 生成按鈕
        const generateBtn = document.getElementById('generate-btn');
        if (generateBtn) {
            generateBtn.addEventListener('click', generateTweets);
        }

        document.addEventListener('keydown', (e) => {
            if (e.key === 'Enter' && e.target.tagName !== 'TEXTAREA' && !e.shiftKey) {
                e.preventDefault();
                generateTweets();
            }
        });

        // 全選/取消全選
        const selectAllCheckbox = document.getElementById('select-all-checkbox');
        if (selectAllCheckbox) {
            selectAllCheckbox.addEventListener('change', (e) => {
                document.querySelectorAll('.tweet-checkbox').forEach(cb => cb.checked = e.target.checked);
                updateSelectionCount();
            });
        }

        // 反選
        const invertBtn = document.getElementById('invert-selection-btn');
        if (invertBtn) {
            invertBtn.addEventListener('click', invertSelection);
        }

        // 監聽checkbox變化以更新計數
        document.addEventListener('change', (e) => {
            if (e.target.classList.contains('tweet-checkbox')) {
                updateSelectionCount();
            }
        });

        // 複製已選
        const copyBtn = document.getElementById('copy-selected-btn');
        if (copyBtn) {
            copyBtn.addEventListener('click', () => {
                const checkedItems = Array.from(document.querySelectorAll('.tweet-checkbox:checked'));
                if (checkedItems.length === 0) {
                    showMessage(TRANSLATIONS[currentLang]['msgSelectCopy']);
                    return;
                }

                const textToCopy = checkedItems.map(cb => cb.closest('.result-item').dataset.content).join('\n\n---\n\n');
                navigator.clipboard.writeText(textToCopy).then(() => {
                    showMessage(TRANSLATIONS[currentLang]['msgCopySuccess'].replace('{count}', checkedItems.length));
                }).catch(err => {
                    console.error('Copy failed:', err);
                    showMessage(TRANSLATIONS[currentLang]['msgCopyFailed']);
                });
            });
        }

        // 導出 Excel/CSV
        const exportBtn = document.getElementById('export-excel-btn');
        if (exportBtn) {
            exportBtn.addEventListener('click', exportToExcel);
        }

        // 導出 TXT
        const exportTxtBtn = document.getElementById('export-txt-btn');
        if (exportTxtBtn) {
            exportTxtBtn.addEventListener('click', exportToText);
        }

        // 監聽滾動事件顯示/隱藏回到頂部按鈕
        window.addEventListener('scroll', () => {
            const backToTop = document.getElementById('back-to-top');
            const resultsContainer = document.getElementById('results-container');

            if (backToTop && resultsContainer && resultsContainer.style.display === 'block' && window.scrollY > 300) {
                backToTop.classList.add('show');
            } else if (backToTop) {
                backToTop.classList.remove('show');
            }
        });

        // 可拖放按鈕事件
        const backToTop = document.getElementById('back-to-top');
        if (backToTop) {
            backToTop.addEventListener('mousedown', dragStart);
            backToTop.addEventListener('mouseup', dragEnd);
            backToTop.addEventListener('mousemove', drag);
            backToTop.addEventListener('touchstart', dragStart);
            backToTop.addEventListener('touchend', dragEnd);
            backToTop.addEventListener('touchmove', drag);
            backToTop.addEventListener('click', scrollToResults);

            // 恢復保存的位置，如果没有则设置默认位置（右下角）
            try {
                const savedX = localStorage.getItem('backToTopX'); // eslint-disable-line no-restricted-globals
                const savedY = localStorage.getItem('backToTopY'); // eslint-disable-line no-restricted-globals
                if (savedX && savedY) {
                    xOffset = parseFloat(savedX);
                    yOffset = parseFloat(savedY);
                } else {
                    // 默认位置：距离右边90px，距离底部20px
                    xOffset = window.innerWidth - 90 - 55/2;
                    yOffset = window.innerHeight - 20 - 55/2;
                }
                setTranslate(xOffset, yOffset, backToTop);
            } catch (e) {
                // localStorage 不可用時設置默認位置
                xOffset = window.innerWidth - 90 - 55/2;
                yOffset = window.innerHeight - 20 - 55/2;
                setTranslate(xOffset, yOffset, backToTop);
            }
        }
    });

</script>
</body>
</html>
