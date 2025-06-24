# -<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <title>學權進度平台</title>
  <style>
    body {
      font-family: "Noto Sans TC", sans-serif;
      margin: 0;
      padding: 20px;
      background-color: #f7f9fc;
      color: #333;
    }
    .page { display: none; }
    .active { display: block; }
    .btn {
      padding: 10px 20px;
      margin: 10px 10px 20px 0;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 6px;
      cursor: pointer;
      font-weight: bold;
    }
    .btn.active {
      background-color: #007bff;
      color: white;
    }
    .case {
      background-color: white;
      border: 1px solid #e0e0e0;
      border-radius: 6px;
      padding: 15px;
      margin-bottom: 10px;
      box-shadow: 0 1px 3px rgba(0,0,0,0.05);
    }
    .case h3 { margin-top: 0; }
    header { margin-bottom: 20px; }
  </style>
</head>
<body>
  <div id="intro" class="page active">
    <header>
      <h1>學權進度平台</h1>
    </header>
    <p>這裡是學生權益案件的追蹤平台，點選下方按鈕查看案件分類。</p>
    <button class="btn" onclick="goToCases()">查看案件列表</button>
  </div>

  <div id="cases" class="page">
    <h2>案件列表</h2>
    <button class="btn" id="btn-autonomous" onclick="filterCases('自主開發案')">自主開發案</button>
    <button class="btn" id="btn-feedback" onclick="filterCases('意見反應案')">意見反應案</button>
    <div id="case-list"></div>
    <button class="btn" onclick="goToIntro()">回首頁</button>
  </div>

  <script>
    const introPage = document.getElementById("intro");
    const casePage = document.getElementById("cases");
    const caseList = document.getElementById("case-list");
    const btnAuto = document.getElementById("btn-autonomous");
    const btnFeedback = document.getElementById("btn-feedback");

    const cases = [
      {
        "案件名稱": "校園增設防蚊液案",
        "案件類型": "意見反應案",
        "受理日期": "2021/03/04",
        "案件大綱": "學生反映宿舍防蚊措施不足，希望於各出入口增設防蚊液供應。",
        "案件結果": "於 3 月中旬於宿舍一樓入口擺放 3 組防蚊液。",
        "狀態": "已完成",
        "結案日期": "2021/05/10"
      },
      {
        "案件名稱": "學生會網站優化",
        "案件類型": "自主開發案",
        "受理日期": "2022/09/01",
        "案件大綱": "希望重整學生會網站 UI 與結構，提升使用者體驗。",
        "案件結果": "設計完成並上線新版網站。",
        "狀態": "已完成",
        "結案日期": "2022/11/15"
      }
    ];

    function goToCases() {
      introPage.classList.remove("active");
      casePage.classList.add("active");
      filterCases("自主開發案");
    }

    function goToIntro() {
      casePage.classList.remove("active");
      introPage.classList.add("active");
    }

    function filterCases(type) {
      btnAuto.classList.toggle("active", type === "自主開發案");
      btnFeedback.classList.toggle("active", type === "意見反應案");

      const filtered = cases.filter(c => c["案件類型"] === type);
      caseList.innerHTML = filtered.map(c => `
        <div class="case">
          <h3>${c["案件名稱"]}</h3>
          <p><strong>受理日期：</strong>${c["受理日期"]}</p>
          <p><strong>案件大綱：</strong>${c["案件大綱"]}</p>
          <p><strong>案件結果：</strong>${c["案件結果"]}</p>
          <p><strong>狀態：</strong>${c["狀態"]}</p>
          <p><strong>結案日期：</strong>${c["結案日期"]}</p>
        </div>
      `).join('');
    }
  </script>
</body>
</html>
