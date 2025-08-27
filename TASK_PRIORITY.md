# 開發任務優先級清單 (Development Task Priority List)

## 🔥 即刻需要處理 (Immediate Action Required)

### P0 - 關鍵功能缺失 (Critical Missing Features)
1. **PDF.js 整合** - 目前編輯器無法載入實際 PDF 檔案
2. **模式切換功能** - 編輯模式與預覽模式切換
3. **設定匯出功能** - 簽名框配置保存與載入

### P1 - 重要改善項目 (Important Improvements)  
1. **簽名框調整大小** - 目前只能移動，無法調整尺寸
2. **資料結構統一** - 編輯器與簽名功能資料格式不一致
3. **狀態管理改善** - 缺乏統一的狀態管理機制

---

## 📋 本週開發計劃 (This Week Development Plan)

### 第一天: PDF.js 整合
- [ ] 研究 PDF.js 最新 API
- [ ] 實作 PDF 檔案選擇和載入
- [ ] 測試不同 PDF 格式相容性
- [ ] 整合到 DesignForm.html

### 第二天: 模式切換系統  
- [ ] 設計模式狀態管理
- [ ] 實作編輯/預覽模式切換
- [ ] 更新 UI 控制項顯示邏輯
- [ ] 加入狀態指示器

### 第三天: 簽名框進階功能
- [ ] 實作調整大小控制點
- [ ] 加入移動邊界限制
- [ ] 改善拖拽視覺回饋
- [ ] 測試多瀏覽器相容性

### 第四天: 設定匯出/匯入
- [ ] 設計 JSON 匯出格式
- [ ] 實作設定儲存功能
- [ ] 實作設定載入功能
- [ ] 加入錯誤處理

### 第五天: 整合測試和優化
- [ ] 端到端功能測試
- [ ] 錯誤處理完善
- [ ] 效能優化
- [ ] 程式碼清理

---

## 🔧 技術實作細節 (Technical Implementation Details)

### PDF.js 整合步驟
```javascript
// 1. 載入 PDF.js 函式庫
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>

// 2. 設定 Worker 路徑
pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';

// 3. 載入 PDF 檔案
async function loadPDF(file) {
    const arrayBuffer = await file.arrayBuffer();
    const pdf = await pdfjsLib.getDocument(arrayBuffer).promise;
    const page = await pdf.getPage(1);
    // 渲染到 Canvas...
}
```

### 模式切換實作
```javascript
// 狀態管理
let currentMode = 'edit'; // 'edit' or 'preview'

function switchMode(mode) {
    currentMode = mode;
    updateUI();
    updateFieldStates();
}

function updateUI() {
    // 根據模式更新介面元素
    if (currentMode === 'edit') {
        showEditControls();
        enableDragDrop();
    } else {
        hideEditControls();
        enableSignature();
    }
}
```

### 資料結構標準化
```javascript
// 統一的簽名框資料格式
const signatureFieldSchema = {
    id: String,           // 唯一識別碼
    type: String,         // 'signature', 'date', 'text'
    x: Number,            // X 座標 (px)
    y: Number,            // Y 座標 (px)  
    width: Number,        // 寬度 (px)
    height: Number,       // 高度 (px)
    text: String,         // 顯示文字
    signed: Boolean,      // 是否已簽名
    signatureData: String // Base64 簽名資料
};
```

---

## 🐛 已知問題和解決方案 (Known Issues & Solutions)

### 問題 1: 拖拽元件在不同螢幕尺寸下位置不準確
**解決方案**: 使用相對座標系統，基於 PDF 頁面比例計算位置

### 問題 2: 簽名畫布在高解析度螢幕上模糊
**解決方案**: 實作 devicePixelRatio 適配

### 問題 3: 觸控裝置上拖拽體驗不佳  
**解決方案**: 加入觸控手勢支援，增大觸控目標

---

## 📊 測試檢查清單 (Testing Checklist)

### 功能測試
- [ ] PDF 載入各種格式測試
- [ ] 拖拽功能跨瀏覽器測試  
- [ ] 簽名畫布在不同裝置測試
- [ ] 設定匯出/匯入正確性測試

### 相容性測試
- [ ] Chrome/Edge/Firefox 測試
- [ ] 桌面/平板/手機響應式測試
- [ ] 高解析度螢幕測試
- [ ] 觸控裝置互動測試

### 效能測試
- [ ] 大型 PDF 檔案載入測試
- [ ] 多個簽名框效能測試
- [ ] 記憶體使用量測試
- [ ] 簽名畫布流暢度測試

---

## 🎯 下週目標 (Next Week Goals)

### Phase 2 準備項目
- [ ] 完成 Phase 1 所有功能
- [ ] 開始資料管理功能設計
- [ ] 本地儲存機制研究
- [ ] 批量操作功能規劃

### 程式碼品質目標
- [ ] 程式碼註釋完善
- [ ] 錯誤處理機制建立
- [ ] 效能最佳化檢查
- [ ] 安全性審查

---

## 📞 支援和資源 (Support & Resources)

### 技術文件
- [PDF.js 官方文件](https://mozilla.github.io/pdf.js/)
- [HTML5 Drag & Drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)
- [Canvas API 參考](https://developer.mozilla.org/en-US/docs/Web/API/Canvas_API)

### 開發工具
- Chrome DevTools for debugging
- Firefox Developer Tools
- VS Code with Live Server extension

---

**建立日期**: 2025-01-XX  
**最後更新**: 2025-01-XX  
**優先級**: P0-P1 本週完成，P2-P3 下週規劃