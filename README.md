
شكرًا لتوضيحك! سأقوم بإعداد لك موقع إلكتروني بسيط باستخدام HTML وCSS وJavaScript يشمل:

1. نموذج لكتابة اسم الزبون ولقبه ورقم هاتفه واختيار الولاية.


2. عرض صور المنتج.


3. حساب السعر الإجمالي تلقائيًا (سعر المنتج + سعر التوصيل حسب الولاية).


4. إرسال الطلب عبر واتساب، مع تضمين المعلومات تلقائيًا في الرسالة.


5. إشعار لك عند إرسال الزبون الطلب (سوف أشرح لك كيفية إضافة هذه الوظيفة في المستقبل في حال أردت التوسع).



سأقوم بتحضير الكود الآن، إليك المثال التالي للموقع:

نموذج HTML مع JavaScript لفتح واتساب:

<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>طلب منتج</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            direction: rtl;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        .container {
            width: 100%;
            max-width: 600px;
            margin: 20px auto;
            background-color: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            font-weight: bold;
            color: #333;
        }
        input, select {
            width: 100%;
            padding: 10px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            width: 100%;
            padding: 15px;
            background-color: #25d366;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #128C7E;
        }
        .product-images {
            text-align: center;
        }
        img {
            max-width: 100%;
            height: auto;
            margin: 10px;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>طلب منتج</h1>
        <div class="product-images">
            <img src="https://via.placeholder.com/500x300?text=Mesure+Cuisine+Électronique" alt="Mesure Cuisine">
        </div>
        
        <div class="form-group">
            <label for="name">الاسم الكامل</label>
            <input type="text" id="name" placeholder="أدخل اسمك">
        </div>

        <div class="form-group">
            <label for="phone">رقم الهاتف</label>
            <input type="tel" id="phone" placeholder="أدخل رقم هاتفك" pattern="[0-9]{10}">
        </div>

        <div class="form-group">
            <label for="state">الولاية</label>
            <select id="state">
                <option value="Algiers">الجزائر</option>
                <option value="Oran">وهران</option>
                <option value="Constantine">قسنطينة</option>
                <option value="Béjaïa">بجاية</option>
                <!-- أضف باقي الولايات هنا -->
            </select>
        </div>

        <div class="form-group">
            <label for="price">سعر المنتج (دج)</label>
            <input type="text" id="price" value="1200" readonly>
        </div>

        <div class="form-group">
            <label for="delivery">سعر التوصيل (دج)</label>
            <input type="text" id="delivery" readonly>
        </div>

        <div class="form-group">
            <label for="total">السعر الإجمالي (دج)</label>
            <input type="text" id="total" readonly>
        </div>

        <button onclick="sendOrder()">إرسال الطلب عبر واتساب</button>
    </div>

    <script>
        const deliveryPrices = {
            "Algiers": 250,
            "Oran": 500,
            "Constantine": 550,
            "Béjaïa": 550,
            // أضف بقية الولايات هنا
        };

        // تحديث سعر التوصيل عند تغيير الولاية
        document.getElementById("state").addEventListener("change", updatePrices);

        function updatePrices() {
            const state = document.getElementById("state").value;
            const price = parseFloat(document.getElementById("price").value);
            const delivery = deliveryPrices[state] || 0;
            const total = price + delivery;

            document.getElementById("delivery").value = delivery;
            document.getElementById("total").value = total;
        }

        function sendOrder() {
            const name = document.getElementById("name").value;
            const phone = document.getElementById("phone").value;
            const state = document.getElementById("state").value;
            const total = document.getElementById("total").value;

            const message = `مرحباً! اسمي ${name} ورقم هاتفي هو ${phone}. أريد طلب منتج "Mesure Cuisine Électronique".  
                            ولاية: ${state}.  
                            السعر الإجمالي: ${total} دج`;

            const whatsappLink = `https://wa.me/0562024381?text=${encodeURIComponent(message)}`;
            window.open(whatsappLink, '_blank');
        }

        // تحديث الأسعار عند تحميل الصفحة
        updatePrices();
    </script>

</body>
</html>

ما يفعله هذا الكود:

1. عرض صور المنتج: صورة مؤقتة للمنتج "Mesure Cuisine Électronique" ستظهر في أعلى الصفحة.


2. نموذج الإدخال:

الاسم الكامل

رقم الهاتف

اختيار الولاية من قائمة منسدلة

سعر المنتج يظهر تلقائيًا

سعر التوصيل حسب الولاية يظهر تلقائيًا



3. حساب السعر الإجمالي: يظهر مباشرة بعد اختيار الولاية.


4. زر إرسال الطلب: عند الضغط عليه، يفتح واتساب مع رسالة تحتوي على جميع تفاصيل الطلب.



ملاحظات:

هذا الموقع قابل للعرض على الهاتف بشكل جيد.

لتشغيله، عليك تحميله على سيرفر ويب أو يمكنك اختبار الملف مباشرة على جهازك بفتح الملف HTML.


هل تحتاج مني مساعدة إضافية في تحميل الموقع أو تخصيصه بشكل أكبر؟

