<template lang="html">

    <BottomNavigation>
        
        <TabStrip>
            <TabStripItem class="navigation__item">
                <Label text="Sign Up"></Label>
            </TabStripItem>
            <TabStripItem class="navigation__item">
                <Label text="Log In"></Label>
            </TabStripItem>
            <TabStripItem class="navigation__item">
                <Label text="Courses"></Label>
            </TabStripItem>
        </TabStrip>

        <TabContentItem>
            <Frame>
                <SignUp/>
            </Frame>
        </TabContentItem>

        <TabContentItem>
            <Frame>
                <LogIn/>
            </Frame>
        </TabContentItem>

        <TabContentItem>
            <Frame>
                <Courses/>
            </Frame>
        </TabContentItem>

    </BottomNavigation>

</template>

<script>

    import SignUp from "./SignUp.vue";
    import LogIn from "./LogIn.vue";
    import Courses from "./Courses.vue";

    export default {
        components: {
            SignUp,
            LogIn,
            Courses
        }
    };

</script>

<style lang="scss">

    .inputext {
        width: 20%
    }

    .input {
        width: 80%
    }

    // Start custom common variables
    @import "~@nativescript/theme/scss/variables/blue";
    // End custom common variables

    // Custom styles

</style>
