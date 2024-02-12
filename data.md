<html>
<div>
<pre id = "data"></pre>
</div>
</html>
<script>
let options = {
    method: 'GET',
    headers: {
        'Content-Type': 'application/json;charset=utf-8',
    },
    credentials: 'include'
}
    fetch("http://127.0.0.1:8008/api/users/", options)
        .then(response => {
            let access = response.status !== 401 && response.status !== 403;
            return response.json().then(data => ({ data, access }));
        })
        .then(({data, access}) => {
            console.log(access)
            if (access){ 
            document.getElementById("data").textContent = JSON.stringify(data, null, 2);
            }
            else {
                document.getElementById("data").textContent = "Unauthorized.";
            }
        })
</script>