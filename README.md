🚫 App बंद करना (instant 😎)

बस JSON edit करो:

{
  "app_status": "blocked",
  "latest_version": 2.1
}

👉 All installed apps → बंद

🛠 Maintenance mode
{
  "app_status": "maintenance",
  "latest_version": 2.1
}
⬆ Future update (force)
{
  "app_status": "active",
  "latest_version": 2.2
}

👉 Old app → unusable


function startAppControl(){

console.log("START CONTROL");

fetch(CONFIG_URL + "?t=" + Date.now())
.then(res => res.json())
.then(data => {

  console.log("DATA:", data);

  if(data.app_status === "blocked"){
    document.body.innerHTML = "🚫 App बंद";
    return;
  }

  if(data.app_status === "maintenance"){
    document.body.innerHTML = "🛠 Maintenance";
    return;
  }

  if(APP_VERSION < data.latest_version){
    document.body.innerHTML = "⬆ Update required";
    return;
  }

  console.log("INIT APP CALL");

  initApp(); // 👈 IMPORTANT

})
.catch((e)=>{
  console.log("ERROR:", e);
  document.body.innerHTML = "🌐 Internet required";
});

}
