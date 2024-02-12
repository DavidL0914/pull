<html>
<div>
<pre id = "data"></pre>
<form>
<input type="text" id = "username" class = "input" placeholder = "username">
<input type="text" id = "uid" class = "input" placeholder = "uid">
</form>
<button class = "submit" onclick = "update()">Change Username</button>
<form>
<input type="text" id = "_uid" class = "input" placeholder = "uid">
</form>
<button class = "submit" onclick = "del()">Delete User</button>
</div>
</html>
<script>
function update() {
    data = {
        "name": document.getElementById("username").value,
        "uid": document.getElementById("uid").value,
        "role": "admin"
    }
    let options = {
    method: 'PUT',
    headers: {
        'Content-Type': 'application/json;charset=utf-8',
    },
    credentials: 'include',
    body: JSON.stringify(data)
}
    fetch("http://127.0.0.1:8008/api/users/", options)
        .then(response => {
            let access = response.status !== 401 && response.status !== 403;
            return response.json().then(data => ({ data, access }));
        })
        .then(({data, access}) => {
            console.log(access)
            if (access){ 
            document.getElementById("data").textContent = "Data Successfully Changed";
            }
            else {
                document.getElementById("data").textContent = "Unauthorized.";
            }
        })
}
function del() {
    data = {
        "uid": document.getElementById("_uid").value,
        "role": "admin"
    }
    let options = {
    method: 'DELETE',
    headers: {
        'Content-Type': 'application/json;charset=utf-8',
    },
    credentials: 'include',
    body: JSON.stringify(data)
}
    fetch("http://127.0.0.1:8008/api/users/", options)
        .then(response => {
            let access = response.status !== 401 && response.status !== 403;
            return response.json().then(data => ({ data, access }));
        })
        .then(({data, access}) => {
            console.log(access)
            if (access){ 
            document.getElementById("data").textContent = "User Successfully Deleted";
            }
            else {
                document.getElementById("data").textContent = "Unauthorized.";
            }
        })
}
</script>