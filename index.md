---
layout: home
search_exclude: true
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Navigation Bar</title>
</head>
<body>

<nav>
    <a href="http://127.0.0.1:4100/frontcasts/signup">Signup</a>
    <a href="http://127.0.0.1:4100/frontcasts/edit">Edit</a>
    <a href="http://127.0.0.1:4100/frontcasts/data">Data</a>
    <a href="http://127.0.0.1:4100/frontcasts/settings">User Settings</a>
    <button onclick = "eraseCookie()">Logout</button>
</nav>

<!-- Your page content goes here -->

</body>
</html>

<script>
    function eraseCookie() {   
        document.cookie = 'jwt=; Max-Age=0; path=/; domain=' + location.hostname;
        console.log(document.cookie) 
        window.location.reload()
}
    let options = {
        method: 'GET',
        headers: {
            'Content-Type': 'application/json;charset=utf-8'
        },
        credentials: 'include'
    }
    function getCookie(name) {
    var match = document.cookie.match(RegExp('(?:^|;\\s*)' + name + '=([^;]*)')); 
    return match ? match[1] : null;
}
    addEventListener("load", (event) => {
        console.log(getCookie("jwt"))
        if(getCookie("jwt")){
            return
        }
        else {
            window.location.href = "http://127.0.0.1:4100/frontcasts/login.html"
        }
    })