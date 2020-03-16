<template lang="html">

    <Page>
        
        <ActionBar title="Log In"/>
        
        <StackLayout>

            <FlexboxLayout flexDirection="row" class="list-group-item">
                <Label class="inputext" text="Username: "/>
                <TextField class="input" hint="Enter username..." autocapitalizationType="none" v-model="username"/>
            </FlexboxLayout>

            <FlexboxLayout flexDirection="row" class="list-group-item">
                <Label class="inputext" text="Password: "/>
                <TextField class="input" hint="Enter password..." secure="true" autocapitalizationType="none" v-model="password"/>
            </FlexboxLayout>

            <Button col="1" row="0" text="Log In" @tap="onButtonTap" />

            <Label col="1" row="0" text="" v-model="message"/>

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
                    url: "https://2116096f.ngrok.io/getUser",
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