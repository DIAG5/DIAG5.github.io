<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>双语交叉PDF生成器</title>
  <script src="https://cdn.jsdelivr.net/npm/pdf-lib@1.17.1/dist/pdf-lib.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/file-saver@2.0.5/dist/FileSaver.min.js"></script>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-50 min-h-screen p-8">
  <div class="max-w-3xl mx-auto bg-white rounded-xl shadow-md p-8">
    <h1 class="text-2xl font-bold text-gray-800 mb-6">📄 双语交叉PDF生成器</h1>
    
    <div class="space-y-4 mb-6">
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-2">第一序列PDF（如中文版）</label>
        <input type="file" id="firstPdf" accept=".pdf" class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-blue-50 file:text-blue-700 hover:file:bg-blue-100">
        <div id="firstPdfInfo" class="mt-1 text-xs text-gray-500"></div>
      </div>
      <div>
        <label class="block text-sm font-medium text-gray-700 mb-2">第二序列PDF（如英文版）</label>
        <input type="file" id="secondPdf" accept=".pdf" class="block w-full text-sm text-gray-500 file:mr-4 file:py-2 file:px-4 file:rounded-full file:border-0 file:text-sm file:font-semibold file:bg-green-50 file:text-green-700 hover:file:bg-green-100">
        <div id="secondPdfInfo" class="mt-1 text-xs text-gray-500"></div>
      </div>
    </div>

    <button id="generateBtn" class="w-full py-3 px-4 bg-indigo-600 hover:bg-indigo-700 text-white font-semibold rounded-lg shadow-md transition-colors disabled:opacity-50 disabled:cursor-not-allowed" disabled>
      生成交叉版PDF
    </button>

    <div id="status" class="mt-4 text-sm text-gray-600"></div>
  </div>

  <script>
    const { PDFDocument } = PDFLib;

    const firstInput = document.getElementById('firstPdf');
    const secondInput = document.getElementById('secondPdf');
    const generateBtn = document.getElementById('generateBtn');
    const status = document.getElementById('status');
    const firstPdfInfo = document.getElementById('firstPdfInfo');
    const secondPdfInfo = document.getElementById('secondPdfInfo');

    // 存储读取后的PDF页数
    let firstPageCount = 0;
    let secondPageCount = 0;

    // 检查文件并读取页数
    async function checkAndReadPdf(input, infoElement, isFirst) {
      if (!input.files[0]) {
        infoElement.textContent = '';
        if (isFirst) firstPageCount = 0;
        else secondPageCount = 0;
        generateBtn.disabled = true;
        return;
      }

      try {
        infoElement.textContent = '正在读取PDF页数...';
        const pdfBytes = await input.files[0].arrayBuffer();
        const pdfDoc = await PDFDocument.load(pdfBytes);
        const pageCount = pdfDoc.getPages().length;
        
        infoElement.textContent = `文件名：${input.files[0].name} | 页数：${pageCount}`;
        
        if (isFirst) firstPageCount = pageCount;
        else secondPageCount = pageCount;

        // 只有两份都读取成功且页数>0才启用按钮
        generateBtn.disabled = !(firstPageCount > 0 && secondPageCount > 0);
      } catch (err) {
        infoElement.textContent = `读取失败：${err.message}`;
        if (isFirst) firstPageCount = 0;
        else secondPageCount = 0;
        generateBtn.disabled = true;
      }
    }

    firstInput.addEventListener('change', () => checkAndReadPdf(firstInput, firstPdfInfo, true));
    secondInput.addEventListener('change', () => checkAndReadPdf(secondInput, secondPdfInfo, false));

    generateBtn.addEventListener('click', async () => {
      try {
        status.textContent = '正在处理PDF...';
        generateBtn.disabled = true;

        // 重新读取文件（避免缓存问题）
        const firstPdfBytes = await firstInput.files[0].arrayBuffer();
        const secondPdfBytes = await secondInput.files[0].arrayBuffer();

        const firstPdfDoc = await PDFDocument.load(firstPdfBytes);
        const secondPdfDoc = await PDFDocument.load(secondPdfBytes);

        const firstPages = firstPdfDoc.getPages();
        const secondPages = secondPdfDoc.getPages();

        // 显示实际读取的页数，方便排查
        status.textContent = `检测到页数：第一序列${firstPages.length}页，第二序列${secondPages.length}页`;

        // 兼容处理：取页数较少的那份作为基准（避免页数不一致时完全无法生成）
        const minPageCount = Math.min(firstPages.length, secondPages.length);
        if (firstPages.length !== secondPages.length) {
          status.textContent += ' → 页数不一致，将按较少页数生成';
        }

        const mergedPdfDoc = await PDFDocument.create();

        // 交叉添加页面（按最少页数处理）
        for (let i = 0; i < minPageCount; i++) {
          // 复制第一序列页面
          const [firstPageCopy] = await mergedPdfDoc.copyPages(firstPdfDoc, [i]);
          mergedPdfDoc.addPage(firstPageCopy);

          // 复制第二序列页面
          const [secondPageCopy] = await mergedPdfDoc.copyPages(secondPdfDoc, [i]);
          mergedPdfDoc.addPage(secondPageCopy);
        }

        // 保存并下载
        const mergedPdfBytes = await mergedPdfDoc.save();
        const blob = new Blob([mergedPdfBytes], { type: 'application/pdf' });
        saveAs(blob, '双语交叉版.pdf');

        status.textContent = '✅ 生成完成！已开始下载';
      } catch (err) {
        status.textContent = `❌ 错误：${err.message}`;
        console.error(err);
      } finally {
        generateBtn.disabled = false;
      }
    });
  </script>
</body>
</html>
