npm i passport passport-local passport-local-mongoose
create model:
    take reference from https://github.com/saintedlama/passport-local-mongoose
    require mongoose
    require passport-local-mongoose
    Schema=mongoose.Schema

    const UserSchema=new Schema({
        email:{
            type:String,
            require:true,
            unique:true
        }
    });

    UserSchema.plugin(passportLocalMongoose);  //this will add field for userId and pw
    module.exports=mongoose.model('User',UserSchema);
create index.js
    require express-session
    require passport
    require passport-local
    require ./models/user

    app.use(session(sesionConfig))
    app.use(passport.initilize())
    app.use(passport.session)
    passport.use(new LocalStrategy(User.authenticate()))

    passport.serializeUser(User.serializeUser());
    passport.deserializeUser(User.deserializeUser());

    app.get('/fakeUser',async(req,res)=>{
        const user=new User({email:asdd@gmail.com',username:'colt'})
        const newUser=await User.register(user,'passport');
    })

