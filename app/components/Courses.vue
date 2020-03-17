<template lang="html">

    <Page>

        <ActionBar title="Search Courses"/>

            <RadSideDrawer ref="drawer">

                <StackLayout ~drawerContent>

                    <Label text="Filter by Topic" class="h2"/>

                    <Button col="1" row="0" text="Math" @tap="addMath"/>

                    <Button col="1" row="0" text="English" @tap="addEnglish"/>

                    <Button col="1" row="0" text="Piano" @tap="addPiano"/>

                    <Button col="1" row="0" text="Reset" @tap="resetFilters"/>

                    <Label text="Sort by Price" class='h2'/>

                    <Button col="1" row="0" text="Sort Price - Ascending" @tap="sortAscend"/>

                    <Button col="1" row="0" text="Sort Price - Descending" @tap="sortDescend"/>

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

    function sortDescending(a, b) {
        if (a.price > b.price) return -1;
        if (a.price < b.price) return 1; return 0;
    }

    function sortAscending(a, b) {
        if (a.price < b.price) return -1;
        if (a.price > b.price) return 1; return 0;
    }

    export default {
        data() {
            return {
                courses: courses,
                searchBar: "",
                filterTopics: [],
            }
        },
        methods: {
            onOpenDrawerTap() {
                this.$refs.drawer.showDrawer();
            },
            onCloseDrawerTap() {
                this.$refs.drawer.closeDrawer();
            },
            sortDescend() {
                console.log("sortDescend pressed.");
                this.courses.sort(sortDescending);
                this.searchBar = " ";
                this.searchBar = "";
            },
            sortAscend() {
                console.log("sortAscend pressed.");
                this.courses.sort(sortAscending);
                this.searchBar = " ";
                this.searchBar = "";
            },
            resetFilters() {
                return this.filterTopics = [];
            },
            addMath() {
                this.filterTopics.push("Math");
            },
            addEnglish() {
                this.filterTopics.push("English");
            },
            addPiano() {
                this.filterTopics.push("Piano");
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
                    var searchCourse = course.topic.toLowerCase().includes(this.searchBar.toLowerCase());
                    var filterCourse = this.filterTopics.length == 0 || this.filterTopics.includes(course.topic);
                    return searchCourse && filterCourse;
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