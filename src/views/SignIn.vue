<template>
    <h1>Sign In to an Acount</h1>
    <p><input type="text" placeholder="Email" v-model="email"></p>
    <p><input type="password" placeholder="Password" v-model="password"></p>
    <p v-if="errMsg" class="bg-yellow-200 text-yellow-800 p-4 rounded-md">{{ errMsg }}</p>
    <p><button @click="login">Submit</button></p>
    <p><button @click="signInWithGoogle">Sign In With Google</button></p>
</template>

<script setup>
import { ref } from 'vue';
import { getAuth, signInWithEmailAndPassword, GoogleAuthProvider, signInWithPopup } from 'firebase/auth';
import { useRouter } from 'vue-router';

const email = ref("");
const password = ref("");
const errMsg = ref("");
const router = useRouter();

const login = () => {
    let auth = getAuth();
    signInWithEmailAndPassword(getAuth(), email.value, password.value)
        .then((data) => {
            console.log("Successfully Signed in!");
            router.push('/feed');
        })
        .catch((error) => {
            console.log(error);
            switch (error.code) {
                case "auth/invalid-email":
                    errMsg.value = "Invalid email";
                    break;
                case "auth/user-not-found":
                    errMsg.value = "No acount with that email was found";
                    break;
                case "auth/wrong-password":
                    errMsg.value = "Incorrect password";
                    break;
                default:
                    errMsg.value = "Email or password was incorrect";
                    break;

            }
        })
}

const signInWithGoogle = () => {
    const provider = new GoogleAuthProvider();
    signInWithPopup(getAuth(), provider)
        .then((result) => {
            console.log(result.user);
            router.push('/feed');
        })
        .catch((error) => {
            console.log("register failed");
        })
}

</script>
