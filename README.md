# Divar_YouTube



let items = document.querySelectorAll('.kt-control-row');
let data = [];

items.forEach(item => {
    let title = item.querySelector('p.kt-control-row__title');
    let description = item.querySelector('div.kt-base-row__description');
    
    data.push({
        title: title ? title.innerText : null,
        description: description ? description.innerText : null
    });
});

// تبدیل داده‌ها به فرمت JSON
let jsonData = JSON.stringify(data, null, 2);

// ایجاد یک عنصر لینک برای دانلود فایل
let downloadLink = document.createElement('a');
downloadLink.href = URL.createObjectURL(new Blob([jsonData], { type: 'application/json' }));
downloadLink.download = 'data.json';

// اضافه کردن لینک به صفحه و کلیک خودکار برای شروع دانلود
document.body.appendChild(downloadLink);
downloadLink.click();
document.body.removeChild(downloadLink);





برای اون فایل شهر هاست باید اسکرول رو خراب کرد
نال پزیر و تبق گفته ها همه چیش اوکی 

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////از هم دیگه جداست

برای اسکرول صفحه ام از این کد استفاده میکنیم

let previousItems = [];

async function autoScroll(element) {
    return new Promise((resolve) => {
        let totalHeight = 0;
        let distance = 100;
        let timer = setInterval(() => {
            element.scrollBy(0, distance);
            totalHeight += distance;

            if (totalHeight >= element.scrollHeight - element.clientHeight) {
                clearInterval(timer);
                resolve();
            }
        }, 100);
    });
}

async function getAllItems() {
    let listElement = document.querySelector('.multi-select-modal__scroll'); // اینجا کلاس المان لیست خود را جایگزین کنید
    await autoScroll(listElement);

    let items = listElement.querySelectorAll('p.kt-control-row__title');
    let values = Array.from(items).map(item => item.innerText);
   
    // اضافه کردن آیتم‌های جدید به آرایه‌ی قبلی
    previousItems = [...previousItems, ...values];

    displayItems(previousItems); // نمایش تمام آیتم‌ها
}

function displayItems(items) {
    console.log("All Items:", items);
}

// فراخوانی تابع برای واکشی همه آیتم‌ها
getAllItems();



///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////از هم دیگه جداست
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////همه استان ها رو میده




let items = document.querySelectorAll('.kt-selector-row');
let result = [];

items.forEach(item => {
    let title = item.querySelector('.kt-selector-row__title').innerText;
    result.push({ value: title });
});

let json = JSON.stringify(result, null, 2);
let blob = new Blob([json], { type: 'application/json' });
let url = URL.createObjectURL(blob);
let link = document.createElement('a');
link.href = url;
link.download = 'data.json';
link.click();
URL.revokeObjectURL(url);

