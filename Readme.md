<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>성과급 재원 책정계획 입력</title>
  <style>
    body {
      font-family: 'Apple SD Gothic Neo', 'Malgun Gothic', dotum, sans-serif;
      padding: 30px;
      background-color: #f4f7f6;
      color: #333;
    }
    .hidden { display: none; }
    .container {
      max-width: 600px;
      margin: auto;
      background: #fff;
      padding: 25px;
      border-radius: 12px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      color: #2c3e50;
      margin-bottom: 25px;
      font-weight: 600;
    }
    
    /* 테이블 스타일 */
    .form-table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 20px;
    }
    .form-table th, .form-table td {
      border: 1px solid #dce4ec;
      padding: 10px;
      text-align: center;
      vertical-align: middle;
    }
    .form-table th {
      background-color: #eaf2f8; /* 연한 파란색 헤더 */
      color: #555;
      font-weight: 600;
    }
    .header-row th {
        background-color: #d6eaf8;
    }
    .label-col {
        background-color: #f9fafc;
        font-weight: 600;
    }
    /* 왼쪽 정렬이 필요한 라벨 */
    .align-left {
        text-align: left;
        padding-left: 15px;
    }
    .sub-text {
        display: block;
        font-size: 0.85em;
        color: #777;
        font-weight: normal;
        margin-top: 4px;
    }

    /* 입력 필드 스타일 */
    input[type="text"],
    input[type="number"],
    input[type="password"],
    input[type="date"],
    textarea {
      width: 100%;
      padding: 10px;
      box-sizing: border-box;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-family: inherit;
      font-size: 14px;
      /* 입력란임을 명확히 하기 위해 배경색 살짝 조정 */
      background-color: #fff; 
    }
    
    /* 이미지처럼 입력란 강조 (선택사항) */
    input:focus, textarea:focus {
      outline: none;
      border-color: #3498db;
      background-color: #ffffe0; /* 포커스 시 연한 노란색 */
    }
    
    textarea {
        resize: vertical; /* 세로 크기 조절 허용 */
    }

    .company-input {
        font-weight: bold;
        color: #2c3e50;
    }

    /* 버튼 스타일 */
    button {
      padding: 12px;
      width: 100%;
      font-size: 16px;
      font-weight: 600;
      background-color: #3498db;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: background-color 0.3s;
      margin-top: 10px;
    }
    button:hover {
      background-color: #2980b9;
    }
    button:disabled {
      background-color: #95a5a6;
      cursor: not-allowed;
    }
    
    /* 유틸리티 */
    .unit-text {
        text-align: right;
        font-size: 12px;
        color: #888;
        margin-bottom: 5px;
    }
    #passwordScreen input { margin-bottom: 15px; }

  </style>
</head>
<body>
  <div class="container">
    <div id="passwordScreen">
      <h2>접속 비밀번호 입력</h2>
      <input type="password" id="passwordInput" placeholder="비밀번호를 입력하세요" />
      <button onclick="checkPassword()">확인</button>
    </div>

    <div id="formScreen" class="hidden">
      <h2>성과급 재원 책정계획</h2>
      
      <table class="form-table">
          <tr>
              <th class="label-col" style="width: 30%;">회사명</th>
              <td>
                  <input type="text" id="company" class="company-input" placeholder="회사명을 입력하세요" />
              </td>
          </tr>
      </table>

      <div class="unit-text">(단위: 백만원)</div>
      
      <table class="form-table">
          <thead>
              <tr class="header-row">
                  <th colspan="2">구분</th>
                  <th style="width: 50%;">2025년 목표/실적</th>
              </tr>
          </thead>
          <tbody>
              <tr>
                  <th rowspan="2" class="label-col">매출</th>
                  <td class="label-col">목표</td>
                  <td><input type="number" id="revTarget" placeholder="0" /></td>
              </tr>
              <tr>
                  <td class="label-col">실적</td>
                  <td><input type="number" id="revActual" placeholder="0" /></td>
              </tr>
              <tr>
                  <th rowspan="2" class="label-col">영업이익<br><span class="sub-text">(성과급 차감 후)</span></th>
                  <td class="label-col">목표</td>
                  <td><input type="number" id="opTarget" placeholder="0" /></td>
              </tr>
              <tr>
                  <td class="label-col">실적</td>
                  <td><input type="number" id="opActual" placeholder="0" /></td>
              </tr>
              <tr>
                  <th class="label-col">성과급</th>
                  <td class="label-col">총액</td>
                  <td><input type="number" id="bonus" placeholder="0" /></td>
              </tr>
          </tbody>
      </table>

      <table class="form-table">
        <thead>
            <tr class="header-row">
                <th style="width: 30%;">구분</th>
                <th>내용</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <th class="label-col align-left">
                    재원 산정 기준
                    <span class="sub-text">(미지급 시 사유 작성)</span>
                </th>
                <td>
                    <textarea id="criteria" rows="4" placeholder="내용을 입력하세요"></textarea>
                </td>
            </tr>
            <tr>
                <th class="label-col align-left">지급 예정일</th>
                <td>
                    <input type="date" id="payDate" />
                </td>
            </tr>
        </tbody>
      </table>

      <button id="submitBtn" onclick="submitData()">제출하기</button>
    </div>
  </div>

  <script>
    const PAGE_PASSWORD = "7603";
    const API_SECRET = "80419372650841793620518467935012"; 
    const WEB_APP_URL = "https://script.google.com/macros/s/AKfycbxH5Y30JrO6pp4KYckOd3-veac_aCcn5O6OI5c4G41cYM0PAtS1N8YgWVfXYFZwETZN/exec";

    function checkPassword() {
      const input = document.getElementById("passwordInput").value;
      if (input === PAGE_PASSWORD) {
        document.getElementById("passwordScreen").classList.add("hidden");
        document.getElementById("formScreen").classList.remove("hidden");
      } else {
        alert("비밀번호가 올바르지 않습니다.");
        document.getElementById("passwordInput").value = "";
        document.getElementById("passwordInput").focus();
      }
    }

    document.getElementById("passwordInput").addEventListener("keypress", function(event) {
      if (event.key === "Enter") {
        event.preventDefault();
        checkPassword();
      }
    });

    function submitData() {
      const btn = document.getElementById("submitBtn");
      const companyVal = document.getElementById("company").value;

      if(!companyVal.trim()) {
        alert("회사명을 입력해주세요.");
        document.getElementById("company").focus();
        return;
      }

      // 데이터 객체 생성 (새로운 필드 criteria, payDate 추가됨)
      const payload = {
        company: companyVal,
        revTarget: document.getElementById("revTarget").value,
        revActual: document.getElementById("revActual").value,
        opTarget: document.getElementById("opTarget").value,
        opActual: document.getElementById("opActual").value,
        bonus: document.getElementById("bonus").value,
        criteria: document.getElementById("criteria").value, // 추가됨
        payDate: document.getElementById("payDate").value,   // 추가됨
        secret: API_SECRET
      };

      btn.disabled = true;
      btn.innerText = "전송 중...";

      fetch(WEB_APP_URL, {
        method: "POST",
        body: JSON.stringify(payload)
      })
      .then(res => res.json())
      .then(data => {
        if(data.result === "success" || data.row) {
          alert("성공적으로 저장되었습니다!");
          // 페이지 새로고침하여 초기화
          location.reload();
        } else {
          alert("저장 실패: " + (data.error || JSON.stringify(data)));
          btn.disabled = false;
          btn.innerText = "제출하기";
        }
      })
      .catch(err => {
        console.error("Error:", err);
        alert("서버 통신 중 오류가 발생했습니다.");
        btn.disabled = false;
        btn.innerText = "제출하기";
      });
    }
  </script>
</body>
</html>
