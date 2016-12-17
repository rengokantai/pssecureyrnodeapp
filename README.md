# pssecureyrnodeapp
##9. Securing Your Connection
###4 Setting up a Secure Server
```
import redirectRequests from "./configurations/redirectRequests";
import open from "open";

const inssecureApp = express();
redirectRequests(insecureApp);
const options = {
  key: fs.readFileSync("server/data/k.key"), //private key
  cert: fs.readFileSync("server/data/k.crt") //cert
};

initialize().then(function(){ 
  insecureApp.listen(insecurePort,function(err){
    if(err){
      console.log(err);
    } else{
      console.log();
      open(`http://${host}:${port}`);
    }
  });
  https.createServer(options,app).listen(443);
})
```

redirectRequests.js
```
const httpsRedirectConfig = (app)=>{
  app.all("*",((req,res,next)=>{
    res.redirect(307,`https://k.com${req.url}`);
  }));
}
export default httpsRedirectConfig;
```
