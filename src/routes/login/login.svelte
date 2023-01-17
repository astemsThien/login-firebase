<script lang="ts">
    // import './css/style.css';
    import { initializeApp } from "firebase/app";
    import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged, createUserWithEmailAndPassword } from "firebase/auth";
    import { onMount } from 'svelte';

    let email = ''; 
    let password = '';
    let user = null;

    const firebaseConfig = {
        apiKey: "AIzaSyDpaJJ09_8vdpRDJsG22OJB75bsx4jwdtg",
        authDomain: "yotube-firebase.firebaseapp.com",
        projectId: "yotube-firebase",
        storageBucket: "yotube-firebase.appspot.com",
        messagingSenderId: "817100251711",
        appId: "1:817100251711:web:20765beceeab731a10ce8a"
    };

    const app = initializeApp(firebaseConfig);
    
    // Login firebase
    const logIn = () => {
        const auth = getAuth(app);
        signInWithEmailAndPassword(auth, email, password)
            .then((userCredential) => {
                user = userCredential.user;
            })
            .catch((error) => {
                const errorCode = error.code;
                const errorMessage = error.message;
                console.log(errorCode, errorMessage);
            });
    };
    // LogOut firebase
    const logOut = async () => {
        const auth = getAuth(app);
        signOut(auth).then(() => {
            user = null;
        });
    };
    // SignUp firebase
    const signUp = () => {
        const auth = getAuth(app);
        createUserWithEmailAndPassword(auth, email, password)
            .then((userCredential) => {
              // Signed in 
                user = userCredential.user;
            })
            .catch((error) => {
                const errorCode = error.code;
                const errorMessage = error.message;
                console.log(errorCode, errorMessage);
            });
    };
    //
    onMount(async () => {
        const auth = getAuth(app);
        onAuthStateChanged(auth, (newUser) => {
            user = newUser;
        });
    })


</script>
<div class="products-breadcrumb">
    <div class="container">
        <ul>
            <li><i class="fa fa-home" aria-hidden="true"></i><a href="/">Home</a><span>|</span></li>
            <li>Sign In & Sign Up</li>
        </ul>
    </div>
</div>
<div class="banner">
    <div class="w3l_banner_nav_center">
<!-- login -->
    <div class="w3_login">
        <h3>Sign In & Sign Up</h3>
        <div class="w3_login_module">
            <div class="module form-module">
            <div class="toggle"><i class="fa fa-times fa-pencil"></i>
                <div class="tooltip">Click Me</div>
            </div>
            <div class="form">
                <h2>Login to your account</h2>
                <form action="#" method="post">
                <input type="email" name="Email" id="email" placeholder="Email" required bind:value={email}>
                <input type="password" name="Password" id="password" placeholder="Password" required bind:value={password}>
                <button class="signIn" on:click={logIn} type="button">Login</button>
                <style>
                    .signIn{
                        width: 100%;
                        background-color: #84c639; 
                        border: 1px solid #84c639;
                        font-size: 25px;
                        color: #ffffff;
                    }
                    .signIn:hover{
                        background-color: #fa1818; 
                    }
                </style>
                </form>
            </div>
            
    
            <div class="form">
                <h2>Create an account</h2>
                <form action="#" method="post">
                <input type="email" name="Email" placeholder="Email Address" required bind:value={email}>
                <input type="password" name="Password" placeholder="Password" required bind:value={password}> 
                <button class="signIn" on:click={signUp} type="button">Register</button>
                </form>
            </div>
            <div class="cta"><a href="/">Forgot your password?</a></div>
            </div>
        </div>
        <script>
            $('.toggle').click(function(){
              // Switches the Icon
            $(this).children('i').toggleClass('fa-pencil');
              // Switches the forms  
            $('.form').animate({
                height: "toggle",
                'padding-top': 'toggle',
                'padding-bottom': 'toggle',
                opacity: "toggle"
            }, "slow");
            });
        </script>
    </div>
    </div>
    <div class="clearfix"></div>
</div>