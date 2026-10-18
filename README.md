<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sách Thơ Điện Tử - redKAI</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@600;700&family=Merriweather:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background: #1a1818;
      background-image: radial-gradient(#2c2828 1px, transparent 0);
      background-size: 24px 24px;
      font-family: 'Merriweather', serif;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 20px;
      color: #2c2c2c;
    }

    .book-container {
      perspective: 1500px;
      width: 100%;
      max-width: 900px;
      display: flex;
      justify-content: center;
      align-items: center;
    }

    .book {
      width: 100%;
      min-height: 550px;
      background: #fbf7f0;
      border-radius: 12px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.5), inset 0 0 100px rgba(0,0,0,0.05);
      display: flex;
      position: relative;
      overflow: hidden;
      border: 12px solid #3d2b1f;
    }

    /* Gáy sách ở giữa */
    .book::before {
      content: '';
      position: absolute;
      left: 50%;
      top: 0;
      bottom: 0;
      width: 30px;
      transform: translateX(-50%);
      background: linear-gradient(to right, rgba(0,0,0,0.15), rgba(0,0,0,0) 40%, rgba(0,0,0,0) 60%, rgba(0,0,0,0.15));
      z-index: 10;
      pointer-events: none;
    }

    .page {
      flex: 1;
      padding: 40px 30px;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
    }

    .page-left {
      border-right: 1px solid rgba(0,0,0,0.08);
      text-align: center;
    }

    .page-right {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }

    .book-title {
      font-family: 'Dancing Script', cursive;
      font-size: 2.8rem;
      color: #8b0000;
      margin-bottom: 10px;
    }

    .author-subtitle {
      font-size: 0.95rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: #666;
      margin-bottom: 30px;
    }

    .decoration {
      color: #b8860b;
      font-size: 1.2rem;
      margin: 15px 0;
    }

    .poem-container {
      text-align: center;
      margin: auto 0;
    }

    .poem-title {
      font-family: 'Dancing Script', cursive;
      font-size: 2.2rem;
      color: #3d2b1f;
      margin-bottom: 25px;
    }

    .poem-content {
      font-size: 1.1rem;
      line-height: 2.2;
      font-style: italic;
      color: #2b2b2b;
    }

    .poem-author {
      margin-top: 25px;
      font-weight: bold;
      font-style: normal;
      font-size: 0.95rem;
      color: #8b0000;
    }

    .page-number {
      font-size: 0.85rem;
      color: #888;
      text-align: center;
    }

    /* Nút bấm chuyển trang */
    .nav-btn {
      position: absolute;
      top: 50%;
      transform: translateY(-50%);
      width: 50px;
      height: 50px;
      background: #3d2b1f;
      color: #fbf7f0;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 1.2rem;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      transition: all 0.3s ease;
      z-index: 20;
    }

    .nav-btn:hover {
      background: #8b0000;
      transform: translateY(-50%) scale(1.1);
    }

    .prev-btn { left: -25px; }
    .next-btn { right: -25px; }

    /* Pop-up Thông báo Lỗi Error Code 367 */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(0, 0, 0, 0.7);
      display: flex;
      justify-content: center;
      align-items: center;
      opacity: 0;
      visibility: hidden;
      transition: all 0.3s ease;
      z-index: 999;
    }

    .modal-overlay.active {
      opacity: 1;
      visibility: visible;
    }

    .error-card {
      background: #fff;
      padding: 30px 40px;
      border-radius: 12px;
      text-align: center;
      max-width: 400px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.3);
      border-top: 6px solid #e74c3c;
      transform: translateY(-20px);
      transition: transform 0.3s ease;
    }

    .modal-overlay.active .error-card {
      transform: translateY(0);
    }

    .error-icon {
      font-size: 3rem;
      color: #e74c3c;
      margin-bottom: 15px;
    }

    .error-code {
      font-size: 1.1rem;
      font-weight: bold;
      color: #7f8c8d;
      margin-bottom: 10px;
      letter-spacing: 1px;
    }

    .error-msg {
      font-size: 1.2rem;
      color: #2c3e50;
      font-weight: 600;
      margin-bottom: 20px;
    }

    .close-btn {
      background: #e74c3c;
      color: white;
      border: none;
      padding: 10px 25px;
      border-radius: 6px;
      font-size: 0.95rem;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.2s;
    }

    .close-btn:hover {
      background: #c0392b;
    }

    /* Custom Responsive cho Mobile */
    @media (max-width: 768px) {
      .book {
        flex-direction: column;
        min-height: auto;
      }
      .book::before { display: none; }
      .page-left {
        border-right: none;
        border-bottom: 1px dashed #ccc;
        padding-bottom: 30px;
      }
      .prev-btn { left: 10px; top: auto; bottom: 10px; transform: none; }
      .next-btn { right: 10px; top: auto; bottom: 10px; transform: none; }
      .prev-btn:hover, .next-btn:hover { transform: scale(1.1); }
    }
  </style>
</head>
<body>

  <div class="book-container">
    <!-- Nút Mũi Tên Sang Trang Trái -->
    <button class="nav-btn prev-btn" id="prevBtn">
      <i class="fa-solid fa-chevron-left"></i>
    </button>

    <!-- Quyển Sách -->
    <div class="book">
      <!-- Trang Trái: Bìa Trong / Tiêu Đề Tập Thơ -->
      <div class="page page-left">
        <div>
          <div class="decoration"><i class="fa-solid fa-feather-pointed"></i></div>
          <h1 class="book-title">Tập Thơ Điện Tử</h1>
          <p class="author-subtitle">Tác giả: redKAI</p>
        </div>
        
        <div class="decoration">❦ ❦ ❦</div>

        <div class="page-number">Trang I</div>
      </div>

      <!-- Trang Phải: Bài Thơ Đầu Tiên -->
      <div class="page page-right">
        <div class="poem-container">
          <h2 class="poem-title">Tri Ân Cô</h2>
          <div class="poem-content">
            Mùa thu ôi đẹp rạng ngời,<br>
            Hoa sữa khoe sắc giữa trời thu sang.<br>
            Hương thơm dịu ngọt nhẹ nhàng,<br>
            Như tình cô dạy mênh mang lòng người.<br>
            Chúc cô luôn nở nụ cười,<br>
            Chèo thuyền tri thức, sáng ngời tương lai.
          </div>
          <p class="poem-author">— Tiến Trường (redKAI)</p>
        </div>
        <div class="page-number">Trang 1</div>
      </div>
    </div>

    <!-- Nút Mũi Tên Sang Trang Phải -->
    <button class="nav-btn next-btn" id="nextBtn">
      <i class="fa-solid fa-chevron-right"></i>
    </button>
  </div>

  <!-- Pop-up Lỗi Code 367 -->
  <div class="modal-overlay" id="errorModal">
    <div class="error-card">
      <div class="error-icon">
        <i class="fa-solid fa-triangle-exclamation"></i>
      </div>
      <div class="error-code">ERROR CODE 367</div>
      <div class="error-msg">Thằng này chưa ra thơ mới</div>
      <button class="close-btn" id="closeBtn">Đóng</button>
    </div>
  </div>

  <script>
    const nextBtn = document.getElementById('nextBtn');
    const prevBtn = document.getElementById('prevBtn');
    const errorModal = document.getElementById('errorModal');
    const closeBtn = document.getElementById('closeBtn');

    // Khi ấn nút Next hoặc Prev thì hiện thông báo lỗi Code 367
    nextBtn.addEventListener('click', showError);
    prevBtn.addEventListener('click', showError);

    function showError() {
      errorModal.classList.add('active');
    }

    // Đóng pop-up khi nhấn nút Đóng hoặc click ra ngoài
    closeBtn.addEventListener('click', () => {
      errorModal.classList.remove('active');
    });

    errorModal.addEventListener('click', (e) => {
      if (e.target === errorModal) {
        errorModal.classList.remove('active');
      }
    });
  </script>
</body>
</html>
