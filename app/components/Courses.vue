<template lang="html">

    <Page>

        <ActionBar title="Search Courses"/>

            <RadSideDrawer ref="drawer">

                <StackLayout ~drawerContent>

                    <Label text="Filter by location" class="h2"/>
                    
                    <!--<ListPicker v-bind="item in items" class="picker"/>-->

                    <Label text="Sort by price" class='h2' />
                    <Label text="Ascending" @tap='sortAscend'/>
                    <Label text="Descending" @tap='sortDescend'/>

                    <Label text="Close Drawer" color="blue" padding="10" style="horizontal-align: center" @tap="onCloseDrawerTap"/>
                    
                </StackLayout>

                <StackLayout ~mainContent>

                    <StackLayout orientation="Vertical">
                        
                        <Button text="Open drawer" @tap="onOpenDrawerTap()"
                        class="drawerContentButton"></Button>

                        <TextField hint="Enter course name..." autocapitalizationType="none" v-model="searchBar"/>

                        <ListView class="list-group" for="course in filteredList">
                            <v-template>
                                <FlexboxLayout flexDirection="row" class="list-group-item">
                                    <Label :text="'Topic: ' + course.topic + ', Price: ' + course.price + ', Location: ' + course.location"/>
                                </FlexboxLayout>
                            </v-template>
                        </ListView>

                    </StackLayout>

                </StackLayout>

            </RadSideDrawer>

    </Page>

</template>

<script>

    import courses from './courses.json';

    import Vue from "nativescript-vue";
    import RadSideDrawer from "nativescript-ui-sidedrawer/vue";
    Vue.use(RadSideDrawer);

    /*fetch("https://2116096f.ngrok.io/courses").then(
        function (response) {
            response.json().then(
                function (text) {
                    this.courses = text,
                    console.log(text);
            });
    })*/

    export default {
        data() {
            return {
                courses: courses,
                searchBar: "",
                userLocations: [],
                title: "Side Drawer example",
                locations: ["hendon", "brent cross", "golders green"]
            }
        },
        methods: {
            onOpenDrawerTap() {
                this.$refs.drawer.showDrawer();
            },
            onCloseDrawerTap() {
                this.$refs.drawer.closeDrawer();
            },
            sortAscend() {
                console.log("sortAscend pressed.");
            },
            sortDescend() {
                console.log("sortDescend pressed.");
            }
        },
        computed: {
            topics: function () { // return an array of all the topics
                return [...new Set(this.filteredList.map(x => x.topic))]
            },
            locations: function () {
                return [...new Set(this.filteredList.map(x => x.location))]
            },
            filteredList() {
                return courses.filter(course => {
                    var searchCourse = course.topic.toLowerCase().includes(this.searchBar);
                    var filterCourse = this.userLocations.length == 0 || this.userLocations.includes(course.location);
                    return searchCourse && filterCourse;
                    //return courses.topic.toLowerCase().includes(this.searchBar.toLowerCase())
                })
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