<script lang="ts">
    import './css/style.css';
    import Login from './login/login.svelte';
    import { initializeApp } from "firebase/app";
    import { getAuth, signInWithEmailAndPassword, signOut, onAuthStateChanged } from "firebase/auth";
    import { onMount } from 'svelte';

    let email = ''; 
    // let username = '';
    // let phone = '';
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
    const signUp = () => {};
    //
    onMount(async () => {
        const auth = getAuth(app);
        onAuthStateChanged(auth, (newUser) => {
            user = newUser;
        });
    })


</script>

<!-- products-breadcrumb -->
{#if user}
<div class="products-breadcrumb">
    <div class="container">
        <ul>
            <li><i class="fa fa-home" aria-hidden="true"></i><a href="/">Home</a><span>|</span></li>
            {#if !user}
            <li>Sign In & Sign Up</li>
            {:else}
            <li><h5>Hi, {user.email}</h5></li>
            {/if}
            <li>
                
                <button class="signOut" on:click={logOut} type="button" style="margin-left: 500px; background-color: #84c639; border: 1px solid #84c639;" >Logout</button>        
            </li>
        </ul>
        
    </div>
</div>
{:else}
                        <Login />
                {/if}
<!-- <Login /> -->


