//1 get-запрос
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>>
<script>
function getUsers() {
    axios.get('https://jsonplaceholder.typicode.com/users')
        .then(response => {
            console.log(response.data);
        });
}
getUsers();

//2 обработка ошибок
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>>
<script>
  function getUsersWithError() {
    axios.get('https://jsonplaceholder.typicode.com/ne-shestvuyushchiy-url')
        .then(response => {
            console.log(response.data);
        })
        .catch(error => {
            console.log(error.message);
        });
}
getUsersWithError();

//3

//4
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
function loadAll() {
    Promise.all([
        axios.get('https://jsonplaceholder.typicode.com/users/1'),
        axios.get('https://jsonplaceholder.typicode.com/posts/1')
    ])
    .then(([userRes, postRes]) => {
        console.log("Пользователь:", userRes.data.name);
        console.log("Пост:", postRes.data.title);
    })
    .catch(error => {
        console.log("4. Один из запросов упал:", error.message);
    });
}
loadAll();
  
//5
  <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>

function loadAllSettled() {
    Promise.allSettled([
        axios.get('https://jsonplaceholder.typicode.com/users/1'),
        axios.get('https://jsonplaceholder.typicode.com/ne-shestvuyushchiy-url') // Упадет в ошибку
    ])
    .then(results => {
        console.log("Результаты allSettled:", results);
    });
}
loadAllSettled();
  
//7
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
function retryRequest(url, retries = 3) {
    axios.get(url)
        .then(response => {
            console.log("Успешно загружено:", response.data);
        })
        .catch(error => {
            if (retries > 0) {
                console.log(`Ошибка, осталось попыток: ${retries}. Повторяем...`);
                retryRequest(url, retries - 1);
            } else {
                console.log("Все попытки исчерпаны:", error.message);
            }
        });
}
retryRequest('https://jsonplaceholder.typicode.com/bad-url');

//9
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<script>
function checkOnlineStatus() {
    axios.get('https://jsonplaceholder.typicode.com/posts/1')
        .then(response => {
            console.log("9. Интернет есть, данные получены");
        })
        .catch(error => {
            if (!navigator.onLine || error.code === "ERR_NETWORK") {
                console.log("Ошибка: Отсутствует подключение к интернету (офлайн)");
            } else {
                console.log("Другая ошибка:", error.message);
            }
        });
}
checkOnlineStatus();
