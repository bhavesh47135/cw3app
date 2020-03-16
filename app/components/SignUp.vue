<template lang="html">

    <Page>
        
        <ActionBar title="Sign Up"/>

        <StackLayout>

            <FlexboxLayout flexDirection="row" class="list-group-item">
                <Label class="inputext" text="E-Mail: "/>
                <TextField class="input" hint="Enter e-mail..." keyboardType="email" autocorrect="false" 
                autocapitalizationType="none" v-model="username"/>
            </FlexboxLayout>

            <FlexboxLayout flexDirection="row" class="list-group-item">
                <Label class="inputext" text="Password: "/>
                <TextField class="input" hint="Enter password..." secure="true" autocapitalizationType="none" v-model="password"/>
            </FlexboxLayout>

            <Button col="1" row="0" text="Sign Up" @tap="onButtonTap" />

            <Label col="1" row="0" text="" v-model="message"/>

            <Label col="1" row="0" textWrap="true" text="To sign up, please make sure you enter a valid email and a password with at least 4 characters."/>

        </StackLayout>

    </Page>
    
</template>

<script>

    import * as http from "http";

    export default {
        data() {
            return {
                username: "",
                password: "",
                message: ""
            };
        },
        methods: {
            onButtonTap() {
                http.request ({
                    url: "https://2116096f.ngrok.io/newUser",
                    method: "POST",
                    headers: { "Content-Type": "application/json" },
                    content: JSON.stringify({
                        username: this.username,
                        password: this.password
                    })
                }).then(response => {
                    var result = response.content.toJSON();
                    this.message = result;
                    console.log(result);
                }, error => {
                    console.error(error);
                });
            }
        }
    };

</script>

<style lang="scss" scoped>

    // Start custom common variables
    @import "~@nativescript/theme/scss/variables/blue";
    // End custom common variables

    // Custom styles

</style>