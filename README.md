let express=require("express")
let mongoose=require("mongoose")
let cors=require("cors")
let multer=require("multer")
let {v4:uuidv4}=require("uuid")
let foodsch=new mongoose.Schema({
    "_id":String,
    "title":String,
    "desc":String,
    "price":Number,
    "cat":String,
    "type":String,
    "qty":String,
    "hotel":String,
    "location":String,
    "rating":Number,
    "img":String

})
let pm=mongoose.model("food",foodsch)
mongoose.connect("mongodb://localhost:27017/v25hfs1fooddb").then(()=>{
    console.log("ok")
})

const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, './pimgs')
  },
  filename: function (req, file, cb) {
    const uniqueSuffix = Date.now() + '-' + Math.round(Math.random() * 1E9)
    cb(null, file.fieldname + '-' + uniqueSuffix+"."+file.mimetype.split("/")[1])
  }
})

const upload = multer({ storage: storage })

let app=express()
app.listen(5000)
app.use(express.urlencoded({"extended":true}))
app.post("/add",upload.single("img"),(req,res)=>{
console.log(req.body)
console.log(req.file)
})
