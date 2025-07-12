<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vape One</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            display: flex;
            height: 100vh;
            flex-direction: column;
        }
        .sidebar {
            width: 25%;
            background-color: #f9f9f9;
            padding: 20px;
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
            position: fixed;
            height: 100%;
            overflow-y: auto;
        }
        .sidebar h2 {
            margin-top: 0;
        }
        .sidebar .input-block {
            margin-bottom: 15px;
        }
        .sidebar .input-block label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .sidebar .input-block input {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        .sidebar button, .sidebar a {
            display: block;
            width: 100%;
            padding: 10px;
            margin: 10px 0;
            text-align: center;
            color: white;
            background-color: #333;
            border: none;
            border-radius: 5px;
            text-decoration: none;
        }
        .sidebar button:hover, .sidebar a:hover {
            background-color: #555;
        }
        .main-content {
            margin-left: 25%;
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        header {
            background-color: #000;
            color: white;
            text-align: center;
            padding: 20px 0;
        }
        nav {
            display: flex;
            justify-content: center;
            background-color: #333;
            padding: 10px 0;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin: 0 15px;
            font-weight: bold;
        }
        nav a:hover {
            text-decoration: underline;
        }
        .products {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-around;
            padding: 20px;
        }
        .product {
            width: 23%;
            margin: 10px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            text-align: center;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .product img {
            width: 100%;
            border-radius: 5px;
        }
        .product:hover {
            transform: scale(1.05);
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
        }
 .product-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
        }
  .product-title {
            font-size: 18px;
            font-weight: bold;
            margin: 10px 0;
        }

        .product-description {
            font-size: 14px;
            color: #555;
            margin-bottom: 10px;
        }

        .popup {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 250px;
            background: white;
            border: 1px solid #ddd;
            border-radius: 10px;
            padding: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            z-index: 10;
        }

        .popup p {
            margin: 0;
            font-size: 14px;
            color: #333;
        }

        .product:hover .popup {
            display: block;
        }

        .view-more-button {
            margin-top: 10px;
            padding: 8px 12px;
            font-size: 14px;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .view-more-button:hover {
            background: #0056b3;
        }

        .popup-button {
            margin-top: 10px;
            padding: 8px 12px;
            font-size: 14px;
            background: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .popup-button:hover {
            background: #218838;
        }

        .popup-description {
            display: none;
            position: absolute;
            bottom: -60px;
            left: 50%;
            transform: translateX(-50%);
            width: 200px;
            padding: 10px;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            font-size: 12px;
            border-radius: 5px;
            text-align: center;
            z-index: 5;
        }

        .popup-button:hover + .popup-description {
            display: block;
        }
        footer {
            background-color: #333;
            color: white;
            text-align: center;
            padding: 20px;
            margin-top: auto;
        }
        .service-btn {
            position: fixed;
            bottom: 20px;
            right: 20px;
            background-color: #000;
            color: white;
            padding: 10px 20px;
            border-radius: 50px;
            text-decoration: none;
            font-weight: bold;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
        }
        .service-btn:hover {
            background-color: #555;
        }
        .top-bar {
            position: fixed;
            top: 0;
            right: 0;
            background-color: #fff;
            padding: 10px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            z-index: 1000;
            display: flex;
            flex-direction: column;
            align-items: flex-end;
        }
        .top-bar .current-cost {
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 10px;
        }
        .cart-items {
            border: 1px solid #ddd;
            padding: 10px;
            border-radius: 5px;
            max-height: 300px;
            overflow-y: auto;
            margin-top: 10px;
        }
        .cart-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            align-items: center;
        }
        .cart-item button {
            background-color: #333;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 3px;
        }
        .cart-item button:hover {
            background-color: #555;
        }
.popup {
    display: none;
    position: absolute;
    top: 50%;
    left: 10%;
    transform: translateY(-50%);
    background: #fff;
    border: 1px solid #ddd;
    border-radius: 5px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    padding: 10px;
    z-index: 100;
    width: 200px;
}
.popup h4 {
    margin: 0 0 10px;
    font-size: 16px;
}
.popup p {
    margin: 0;
    font-size: 14px;
    color: #555;
}
.product:hover .popup {
    display: block;
}
    </style>
</head>
<body>
<h1 style="text-align: center;">주의! 니코틴은 신체에 해롭습니다</h1>
    <div class="sidebar">
        <h2>로그인 / 회원가입</h2>
        <div class="input-block">
            <label for="userId">ID</label>
            <input type="text" id="userId" name="userId" placeholder="아이디 입력">
        </div>
        <div class="input-block">
            <label for="userPassword">Password</label>
            <input type="password" id="userPassword" name="userPassword" placeholder="비밀번호 입력">
        </div>
        <button id="loginBtn">로그인</button>
        <button id="signupBtn">회원가입</button>
        <button id="phoneAuthBtn" class="hidden">휴대폰 인증</button>
        <script>
            document.getElementById("signupBtn").addEventListener("click", function () {
                document.getElementById("phoneAuthBtn").classList.remove("hidden");
            });
            document.getElementById("phoneAuthBtn").addEventListener("click", function () {
                window.location.href = "https://example.com/phone-auth";
            });
        </script>
        <h3>공지사항</h3>
        <p>베이프 원 만의 독보적인 이벤트!</p>
        <h3>이벤트</h3>
        <p>현재 진행중인 다양한 이벤트</p>
        <h3>제품 후기</h3>
        <p>리뷰 쓰고 쿠폰 받아가세요.</p>
    </div>
    <div class="main-content">
        <div class="top-bar">
            <span class="current-cost">Total Cost: $<span id="total-cost">0</span></span>
            <input type="text" id="search" placeholder="Search products...">
            <div class="cart-items" id="cart-items"></div>
        </div>
        <header>
            <h1>Vape One</h1>
            <p>원하는 전자담배가 집 앞에!</p>
        </header>
        <nav>
            <a href="#about">회사 소개</a>
            <a href="#products">제품</a>
            <a href="#contact">문의하기</a>
        </nav>
        <div class="products">
            <div class="product" data-name="Blueberry Vape">
                <img src="https://via.placeholder.com/150" alt="Blueberry Vape">
                <h3>Blueberry Vape</h3>
                <p>$20</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Strawberry Vape">
                <img src="https://via.placeholder.com/150" alt="Strawberry Vape">
                <h3>Strawberry Vape</h3>
                <p>$22</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Mango Vape">
                <img src="https://via.placeholder.com/150" alt="Mango Vape">
                <h3>Mango Vape</h3>
                <p>$18</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Watermelon Vape">
                <img src="https://via.placeholder.com/150" alt="Watermelon Vape">
                <h3>Watermelon Vape</h3>
                <p>$25</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Grape Vape">
                <img src="https://via.placeholder.com/150" alt="Grape Vape">
                <h3>Grape Vape</h3>
                <p>$19</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Pineapple Vape">
                <img src="https://via.placeholder.com/150" alt="Pineapple Vape">
                <h3>Pineapple Vape</h3>
                <p>$23</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Coconut Vape">
                <img src="https://via.placeholder.com/150" alt="Coconut Vape">
                <h3>Coconut Vape</h3>
                <p>$21</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Peach Vape">
                <img src="https://via.placeholder.com/150" alt="Peach Vape">
                <h3>Peach Vape</h3>
                <p>$20</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Apple Vape">
                <img src="https://via.placeholder.com/150" alt="Apple Vape">
                <h3>Apple Vape</h3>
                <p>$22</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Cherry Vape">
                <img src="https://via.placeholder.com/150" alt="Cherry Vape">
                <h3>Cherry Vape</h3>
                <p>$24</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Lemon Vape">
                <img src="https://via.placeholder.com/150" alt="Lemon Vape">
                <h3>Lemon Vape</h3>
                <p>$18</p>
                <button class="add-to-cart">Add to Cart</button>
<div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
            <div class="product" data-name="Raspberry Vape">
                <img src="https://via.placeholder.com/150" alt="Raspberry Vape">
                <h3>Raspberry Vape</h3>
                <p>$26</p>
                <button class="add-to-cart">Add to Cart</button>
 <div class="popup">
        <h4>Blueberry Vape</h4>
        <p>상쾌한 블루베리 향과 부드러운 증기.</p>
    </div>
            </div>
        </div>
        <footer>
            <p>&copy; 2024 VAPE ONE. All Rights Reserved.</p>
        </footer>
    </div>
    <script>
        const totalCostElement = document.getElementById('total-cost');
        const cartItemsContainer = document.getElementById('cart-items');
        let totalCost = 0;

        document.querySelectorAll('.add-to-cart').forEach(button => {
            button.addEventListener('click', function () {
                const product = this.parentElement;
                const name = product.getAttribute('data-name');
                const price = parseInt(product.querySelector('p').textContent.replace('$', ''));
                addToCart(name, price);
            });
        });

        function addToCart(name, price) {
            let existingItem = Array.from(cartItemsContainer.children).find(
                item => item.dataset.name === name
            );

            if (existingItem) {
                const quantityElement = existingItem.querySelector('.quantity');
                quantityElement.textContent = parseInt(quantityElement.textContent) + 1;
            } else {
                const cartItem = document.createElement('div');
                cartItem.className = 'cart-item';
                cartItem.dataset.name = name;

                const itemInfo = document.createElement('span');
                itemInfo.textContent = `${name} - $${price}`;

                const quantityElement = document.createElement('span');
                quantityElement.className = 'quantity';
                quantityElement.textContent = '1';

                const increaseButton = document.createElement('button');
                increaseButton.textContent = '+';
                increaseButton.addEventListener('click', function () {
                    totalCost += price;
                    totalCostElement.textContent = totalCost;
                    quantityElement.textContent = parseInt(quantityElement.textContent) + 1;
                });

                const decreaseButton = document.createElement('button');
                decreaseButton.textContent = '-';
                decreaseButton.addEventListener('click', function () {
                    const currentQuantity = parseInt(quantityElement.textContent);
                    if (currentQuantity > 1) {
                        quantityElement.textContent = currentQuantity - 1;
                        totalCost -= price;
                        totalCostElement.textContent = totalCost;
                    } else {
                        totalCost -= price;
                        totalCostElement.textContent = totalCost;
                        cartItemsContainer.removeChild(cartItem);
                    }
                });

                cartItem.appendChild(itemInfo);
                cartItem.appendChild(quantityElement);
                cartItem.appendChild(increaseButton);
                cartItem.appendChild(decreaseButton);
                cartItemsContainer.appendChild(cartItem);
            }

            totalCost += price;
            totalCostElement.textContent = totalCost;
        }
    </script>
   </footer>
    </div>
    <a href="https://pf.kakao.com/_YourChannelCode/chat" class="service-btn" target="_blank">
        1:1 카카오톡 상담하기
    </a>
</body>
</html>
