# 🚀 Useful_component_for_web_project

## Frontend Support
### Responsive React Image Slider (Framer Motion + Swipe Support)

```bash
# Install dependencies
npm install framer-motion react-swipeable
```

```jsx
    import React, { useState, useEffect, useRef } from "react";
    import { motion, AnimatePresence } from "framer-motion";
    import { useSwipeable } from "react-swipeable";

    import b1 from '../assets/mb1.png'
    import b2 from '../assets/mb2.png'
    import b3 from '../assets/mb3.png'
    import b4 from '../assets/mb4.png'
    import b5 from '../assets/mb5.png'


    const banners = [
    { 
        id: 1, 
        title: "New Collection", 
        desc: "Discount 50% for the first transection", 
        btnText: "Shop now", 
        bgColor: "bg-[#EDE6DA]", 
        textColor: "text-[#171417]", 
        buttonBgColor: "bg-[#6D503A]", 
        img: b1, 
    },
    {
        id: 2,
        title: "Elegant Diamond",
        desc: "Sparkle brighter with our latest diamond collection",
        btnText: "Explore now",
        bgColor: "bg-[#F5EDE3]",
        textColor: "text-[#2A1B10]",
        buttonBgColor: "bg-[#A37B4E]",
        img: b2
    },
    {
        id: 3,
        title: "Golden Heritage",
        desc: "Pure gold jewellery handcrafted for your royal look",
        btnText: "Discover more",
        bgColor: "bg-[#FFF8E7]",
        textColor: "text-[#3B2A1A]",
        buttonBgColor: "bg-[#B88A44]",
        img: b3
    },
    {
        id: 4,
        title: "Silver Serenity",
        desc: "Minimal designs for everyday elegance",
        btnText: "Shop collection",
        bgColor: "bg-[#F4F4F4]",
        textColor: "text-[#2C2C2C]",
        buttonBgColor: "bg-[#8C8C8C]",
        img: b4
    },
    {
        id: 5,
        title: "Rose Gold Romance",
        desc: "Fall in love with our exclusive rose gold jewellery",
        btnText: "View collection",
        bgColor: "bg-[#F9E8E4]",
        textColor: "text-[#3D2B2B]",
        buttonBgColor: "bg-[#C1866A]",
        img: b5
    }

    ]


    const Banner = () => {
    const [index, setIndex] = useState(0);
    const [paused, setPaused] = useState(false);
    const intervalRef = useRef(null);

    // Auto slide control
    useEffect(() => {
        if (!paused) {
        intervalRef.current = setInterval(() => {
            setIndex((prev) => (prev + 1) % banners.length);
        }, 4000);
        }
        return () => clearInterval(intervalRef.current);
    }, [paused]);

    // Swipe control
    const handlers = useSwipeable({
        onSwipedLeft: () => setIndex((prev) => (prev + 1) % banners.length),
        onSwipedRight: () => setIndex((prev) => (prev - 1 + banners.length) % banners.length),
        trackMouse: true,
    });

    return (
        <div className="px-2 mt-3">
        <div
        className="relative w-full max-w-4xl overflow-hidden rounded-2xl shadow-lg h-40"
        {...handlers}
        onMouseEnter={() => setPaused(true)}   // Pause when hovered
        onMouseLeave={() => setPaused(false)} // Resume when mouse leaves
        >
        <AnimatePresence>
            <motion.div
            key={banners[index].id}
            className={`absolute inset-0 flex items-center justify-between text-white ${banners[index].bgColor}`}
            initial={{ opacity: 0, x: 100 }}
            animate={{ opacity: 1, x: 0 }}
            exit={{ opacity: 0, x: -100 }}
            transition={{ duration: 0.6 }}
            >
            {/* Left Section */}
            <div className="flex flex-col justify-between h-full max-w-sm p-6">
                <h2 className={`text-xl font-semibold leading-snug ${banners[index].textColor}`}>
                {banners[index].title}
                </h2>
                <p className={`text-[12.5px] mt-1 ${banners[index].textColor}`}>{banners[index].desc}</p>
                <button className={`w-28 text-white rounded-md shadow-md py-2 mt-4 text-[12px] font-bold hover:bg-neutral-700 transition ${banners[index].buttonBgColor}`}>
                {banners[index].btnText}
                </button>
            </div>

            {/* Right Image */}
            <div className="w-1/2 h-full">
                <img
                src={banners[index].img}
                alt={banners[index].title}
                className="w-full h-full object-cover rounded-r-2xl"
                />
            </div>
            </motion.div>
        </AnimatePresence>
        </div>
        
        {/* Dots Indicator */}
        
        <div className="absolute pt-3 left-1/2 -translate-x-1/2 flex gap-2">
            {banners.map((_, i) => (
            <div
                key={i}
                onClick={() => setIndex(i)}
                className={`w-2 h-2 rounded-full cursor-pointer transition-all ${
                i === index ? "bg-[#7B542F] scale-125" : "bg-[#E6D8C3]"
                }`}
            />
            ))}
        </div>
        </div>
    );
    };

    export default Banner;

```

### Hiding scrollar using css
```css
.scroll-hide{
    -ms-overflow-style: none;
    scrollbar-width: none;
}
```
### Showing text in one line

```css 
.line-clamp-2 {
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

```

### Card Skeleton using react

```jsx
import React from 'react'

const CardSkeleton = () => {
  return (
    <div className='w-full min-h-70 max-w-md p-4 rounded-xl shadow-xs flex flex-col gap-y-2'>
      <div className='w-full h-60 skeleton rounded-xl'></div>
      <div className='flex flex-col gap-y-3 md:mt-6'>
        <div className='h-4 w-11/12 skeleton rounded'></div>
        <div className='h-4 w-11/12 skeleton rounded'></div>
        <div className='h-4 w-11/12 skeleton rounded'></div>
      </div>
    </div>
  )
}

export default CardSkeleton

```
```css
@layer utilities{
  .skeleton{
    @apply bg-[#f8f1eb] relative overflow-hidden
  }
  .skeleton::after{
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    height: 100%;
    width: 100%;
    background: linear-gradient(90deg, transparent, #FCFDF5, transparent);
    animation: shimmer 1.3s infinite;
  }
  @keyframes shimmer {
    100%{
      transform: translateX(100%);
    }
  }
}
```

### Form handle in react
```jsx
import React, { useState } from "react";
function App() {
const [formData, setFormData] = useState({ name: "", email: "" });
const handleChange = (e) => {
  setFormData({ ...formData, [e.target.id]: e.target.value });
};
const handleSubmit = (e) => {
  e.preventDefault(); // Prevents page reload
  console.log("Form Data Submitted:", formData);
};
 return (
  <form onSubmit={handleSubmit}>
    {state === 'signup' && (
      <input
        id='name'
        type='text'
        placeholder='Full Name'
        value={formData.name}
        onChange={handleChange}
        required
      />
    )}

    <input
      id='email'
      type='email'
      placeholder='Enter your email'
      value={formData.email}
      onChange={handleChange}
      required
    />

    <button type='submit'>
      login
    </button>
  </form>
 );
}
export default App;
```

### Picture upload in react
```js
<div className='flex items-center gap-4 mb-8 text-gray-500'>
  <label htmlFor="img">
      <img src={docImg ? URL.createObjectURL(docImg) : assets.upload_area} alt="" />
  </label>
  <input onChange={(e)=>setDocImg(e.target.files[0])} type="file" id='img' hidden />
  <p>Upload picture</p>
</div>
```

## Backend Support
```bash
# Install dependencies
npm install express cors dotenv jsonwebtoken cloudinary bcryptjs cookie-parser mongoose multer svix socket.io passport pg prisma sequelize passport-google-oauth20
```
### Allowed the origins in server 
```js
const allowedOrigins = [
  "http://localhost:5173",
  "http://localhost:5174"
];

app.use(
  cors({
    origin: function (origin, callback) {
      // Allow requests with no origin (like Postman)
      if (!origin) return callback(null, true);

      if (allowedOrigins.includes(origin)) {
        callback(null, true);
      } else {
        callback(new Error("Not allowed by CORS"));
      }
    },
    credentials: true,
  })
);

```

### Login, Register and Logout using Cookie-Perser

```js
export const register = async(req, res)=>{
    try {
        const {fullName, email, password, bio} = req.body;
        if(!fullName || !email || !password || !bio){
            return res.json({success: false, message: "Missing Details"})
        }

        const existingUser = await user.findOne({email})
        if(existingUser){
            return res.json({success: false, message: "User already exist"})
        }
        const hashedPassword = await bcrypt.hash(password, 10);
        const newUser = new user({
            fullName,
            email,
            password: hashedPassword,
            bio
        })
        await newUser.save()
        const token = jwt.sign({id: newUser._id}, process.env.JWT_SECRET, { expiresIn: '7d' });
        res.cookie('token', token,{
            httpOnly: true,
            secure: true,
            sameSite: 'None',
            maxAge: 7*24*60*60*1000
        })
        return res.json({success: true, message:"Register Successfull", token})

    } catch (error) {
        return res.json({success: false, message: error.message})
    }
}

export const login = async(req, res)=>{
    try {
        const {email, password} = req.body;
        if(!email || !password){
            return res.json({success: false, message: "Missing Details"})
        }

        const existingUser = await user.findOne({email});
        if(!existingUser){
            return res.json({success: false, message: "User not found"})
        }
        const isMatch = await bcrypt.compare(password, existingUser.password)
        if(!isMatch){
            return res.json({success:false, message: 'Wrong Password'});
        }

        const token = jwt.sign({id: existingUser._id}, process.env.JWT_SECRET, { expiresIn: '7d' });
        res.cookie('token', token,{
            httpOnly: true,
            secure: true,
            sameSite: 'None',
            maxAge: 7*24*60*60*1000
        })
        return res.json({success: true, message:"Welcom Back", token})

    } catch (error) {
        return res.json({success: false, message: error.message})
    }
}

export const logout = async(req, res)=>{
    try {
        res.clearCookie('token', {
            httpOnly:true,
            secure: true,
            sameSite: 'None',
        })
        return res.json({success:true, message: 'Logout Successfully'})
    } catch (error) {
        return res.json({success:false, message: error.message})
    }
}
```

### User Authentication Middleware

```js
import jwt from 'jsonwebtoken'

const isAuth = async(req, res, next)=>{
    try {
        const {token} = req.cookies;

        if(!token){
            return res.json({success: false, message:'did not find token'})
        }

        const tokenDecode = jwt.verify(token, process.env.JWT_SECRET);
        if(tokenDecode.id){
            req.userId = tokenDecode.id;
        } else{
            return res.json({ success: false, message: "Not authorized" });
        }
        next();
    } catch (error) {
        return res.json({success: false, message:error.message})
    }
}

export default isAuth
```

### Image Upload in cloudinary

```js
import {v2 as cloudinary} from 'cloudinary'

const connectCloudinary = async()=>{
    cloudinary.config({
        cloud_name: process.env.CLOUDINARY_CLOUD_NAME,
        api_key: process.env.CLOUDINARY_API_KEY,
        api_secret: process.env.CLOUDINARY_API_SECRET
    })
}
export default connectCloudinary;
```

### Storage in multer

```js
import multer from 'multer'

const storage = multer.diskStorage({
    filename: function(req, file, callback){
        callback(null, file.originalname)
    }
})

const upload = multer({storage})

export default upload;
```

### MongoDb database create

```js
import mongoose from "mongoose";

const dbConnect = async()=>{
    mongoose.connection.on('connected', ()=>
    console.log("Database Connected"))

    await mongoose.connect(process.env.MONGODB_URI)
}

export default dbConnect
```

## User authentication using clerk

```js
import { Webhook } from 'svix'
import UserModel from '../models/userModel.js'

// APi controller function

export const clerkWebhooks = async(req, res)=>{
    try {
        // create a svix instance with clerk 
        const whook = new Webhook (process.env.CLERK_WEBHOOK_SECRET)
        

        //verifying headers
        await whook.verify(JSON.stringify(req.body),{
        "svix-id": req.headers["svix-id"],
        "svix-timestamp": req.headers["svix-timestamp"],
        "svix-signature": req.headers["svix-signature"]
        })

        // getting data from request body
         const { data, type } = req.body

        //switch-case statement

        switch (type) {
            case 'user.created':{
                const userData = {
                    _id: data.id,
                    email: data.email_addresses[0].email_address,
                    name:data.first_name + " " + data.last_name,
                    image: data.image_url,
                    address:[],
                    cart:[],
                    orderHistory:[]
                }
                await UserModel.create(userData);
                return res.status(201).json({ success: true })
            }
            case 'user.updated':{
                const userData = {
                    email: data.email_addresses[0].email_address,
                    name:data.first_name + " " + data.last_name,
                    image: data.image_url,
                }
                await UserModel.findByIdAndUpdate(data.id, userData)
                return res.status(200).json({ success: true })
            }
            case 'user.deleted':{
                await UserModel.findByIdAndDelete(data.id)
                res.json({})
                return res.status(200).json({ success: true })
            }
            default:
                return res.status(400).json({ success: false, message: "Unhandled webhook type" })
            
        }
    } catch (error) {
        console.log(error.message)
        res.json({success:false, message:'webhooks error'})
    }
}
```

## Frontend for clerk auth

```bash
# Install dependencies
npm install @clerk/clerk-react
```
```ini
# Add Clerk Publishable Key .env
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
```
`main.jsx`
```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App.jsx";
import { ClerkProvider } from "@clerk/clerk-react";

const PUBLISHABLE_KEY = import.meta.env.VITE_CLERK_PUBLISHABLE_KEY;

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <ClerkProvider publishableKey={PUBLISHABLE_KEY}>
      <App />
    </ClerkProvider>
  </React.StrictMode>
);

```
`App.jsx`
```jsx
import React from "react";
import { BrowserRouter, Routes, Route } from "react-router-dom";
import { SignIn, SignUp, SignedIn, SignedOut, RedirectToSignIn } from "@clerk/clerk-react";

import Home from "./pages/Home.jsx";
import Dashboard from "./pages/Dashboard.jsx";

const App = () => {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />

        {/* Auth Routes */}
        <Route path="/sign-in/*" element={<SignIn routing="path" path="/sign-in" />} />
        <Route path="/sign-up/*" element={<SignUp routing="path" path="/sign-up" />} />

        {/* Protected Route */}
        <Route
          path="/dashboard"
          element={
            <>
              <SignedIn>
                <Dashboard />
              </SignedIn>
              <SignedOut>
                <RedirectToSignIn />
              </SignedOut>
            </>
          }
        />
      </Routes>
    </BrowserRouter>
  );
};

export default App;

```

`Home.jsx`
```jsx
import React from "react";
import { Link } from "react-router-dom";
import { UserButton, SignedIn, SignedOut } from "@clerk/clerk-react";

const Home = () => {
  return (
    <div style={{ padding: 20 }}>
      <h2>Welcome to our App 👋</h2>

      <SignedOut>
        <Link to="/sign-in">Login</Link> | <Link to="/sign-up">Register</Link>
      </SignedOut>

      <SignedIn>
        <UserButton /> <br /><br />
        <Link to="/dashboard">Go to Dashboard</Link>
      </SignedIn>
    </div>
  );
};

export default Home;

```
`Dashboard.jsx`
```jsx
import React from "react";
import { useUser, UserButton } from "@clerk/clerk-react";

const Dashboard = () => {
  const { user } = useUser();

  return (
    <div style={{ padding: 20 }}>
      <UserButton />
      <h2>Dashboard</h2>
      <p>Welcome {user?.fullName}</p>
      <img src={user?.imageUrl} alt="" width={80} style={{borderRadius:"50%"}} />
      <p>Email: {user?.primaryEmailAddress?.emailAddress}</p>
    </div>
  );
};

export default Dashboard;

```

## User authentication using Google oauth
### Backend
`Passport.js`
```js

import passport from "passport";
import { Strategy as GoogleStrategy } from "passport-google-oauth20";
import {User} from "../models/User.js";

passport.use(
  new GoogleStrategy(
    {
      clientID: process.env.GOOGLE_CLIENT_ID,
      clientSecret: process.env.GOOGLE_CLIENT_SECRET,
      callbackURL: `${process.env.BACKEND_URL}/auth/google/callback`,
    },
    async (accessToken, refreshToken, profile, done) => {
      try {
        // Check if user exists
        let user = await User.findOne({ googleId: profile.id });

        if (!user) {
          // Create new user
          user = await User.create({
            googleId: profile.id,
            name: profile.displayName,
            email: profile.emails[0].value,
            picture: profile.photos[0].value,
          });
        }

        return done(null, user);
      } catch (err) {
        return done(err, null);
      }
    }
  )
);

passport.serializeUser((user, done) => done(null, user.id));
passport.deserializeUser(async (id, done) => {
  const user = await User.findById(id);
  done(null, user);
});

export default passport;
```

`AuthController.js`
```js

// ======== Google Login Controllers =======
export const googleLogin = (req, res) => {
  res.send("Redirecting to Google...");
};

export const googleCallback = (req, res) => {
  // req.user is set by Passport session
  if (!req.user) return res.redirect(`${process.env.CLIENT_URL}/login`);

  // Optionally: issue a JWT for frontend
  const token = jwt.sign({ id: req.user._id }, process.env.JWT_SECRET, { expiresIn: "1d" });
  res.cookie("token", token, {
    httpOnly: true,
    secure: process.env.NODE_ENV === "production",
    sameSite: "None",
    maxAge: 24 * 60 * 60 * 1000,
  });

  res.redirect(process.env.CLIENT_URL);
};


export const loginFailure = (req, res) => {
  res.status(401).json({ success: false, message: "Failed to authenticate with Google" });
};

// controllers/authController.js

export const logoutUser = (req, res) => {
  req.logout(function(err) {
    if (err) return res.status(500).json({ success: false, message: "Logout failed" });
    req.session.destroy(() => {
      res.clearCookie("connect.sid"); // Passport session cookie
      res.clearCookie("token"); // JWT cookie
      return res.status(200).json({ success: true, message: "Logged out successfully" });
    });
  });
};


export const getUser = async (req, res) => {
  try {
    if (req.user) {
      // Google user (via Passport session)
      return res.json({ success: true, user: req.user });
    }

    // JWT user
    const token = req.cookies.token;
    if (!token) return res.json({ success: false, user: null });

    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    const user = await User.findById(decoded.id).select("-password");
    if (!user) return res.json({ success: false, user: null });

    return res.json({ success: true, user });
  } catch (err) {
    console.error(err);
    res.json({ success: false, user: null });
  }
};

```

`middleware.js`
```js
import jwt from "jsonwebtoken";

export const getUserIdFromToken = (req, res, next) => {
  // Priority: Passport session user (Google) -> JWT token
  if (req.user) {
    req.userId = req.user._id;
    return next();
  }

  const token = req.cookies?.token;
  if (!token) return res.status(401).json({ success: false, message: "Unauthorized" });

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.userId = decoded.id;
    next();
  } catch (err) {
    return res.status(401).json({ success: false, message: "Invalid token" });
  }
};

```
`authRoute.js`
```js
// Step 1: Start Google OAuth
router.get("/google", passport.authenticate("google", { scope: ["profile", "email"] }));

// Step 2: Google callback URL
router.get(
  "/google/callback",
  passport.authenticate("google", { failureRedirect: "/auth/login/failure" }),
  googleCallback
);

// ========== Other routes ========
router.get("/login/failure", loginFailure);
router.get("/logout", logoutUser);
router.get("/user", getUser);
```
`in server add this`

```js
// Session setup (required for Passport + Google Auth)
app.use(
  session({
    secret: process.env.SESSION_SECRET || "supersecretkey",
    resave: false,
    saveUninitialized: false,
    cookie: {
      secure: process.env.NODE_ENV === "production", // production only true in prod (HTTPS)
      sameSite: "None", // required when frontend on different domain
      httpOnly: true,
    },
  })
);

```

`frontend`
```js
const handleGoogleLogin = () => {
  window.open(`${backendUrl}/auth/google`, "_self");
};
```

