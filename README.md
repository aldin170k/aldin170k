
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
