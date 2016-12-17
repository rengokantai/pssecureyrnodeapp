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
###6 Introducing to HTTP Strict Transport Security
####HTTP strict transport security  
HTTP header to notify supporting browsers that future requests to this site should be made over HTTPS


###7 Implementing the HSTS Header
responseHeaderConfig.js
```
const responseHeaderConfig = (app) => {
  app.use((req,res,next)=>{
    const maxAge = 60*60*24*365;
    res.set("Strict-Transport-Security",`max-age=${maxAge}; includeSubdomains; preload`);
    next();
  })
}
```
