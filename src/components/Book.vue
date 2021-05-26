<template>
    <div class="hello">
        <!-- <h1>{{ msg }}</h1>
    <h2>{{ count }}</h2>
    <button v-on:click="count++">Add + 1</button> -->
        <div>
            <p>What type of books to look for?</p>
            <input v-model="category" v-on:keyup.enter="getName" />
            <!-- <div v-for="book in data" :key="book.id">
					<h3>{{ book.name }}</h3>
					<img :src="book.picture" />
				</div> -->

            <div v-if="loaded && data.length != currentElement" class="book">
                <p>{{ data[currentElement].name }}</p>
                <img :src="data[currentElement].picture" />
            </div>
            <div v-else class="book">
                <p>Enter more to discover more</p>
            </div>
            <div v-if="data.length != currentElement">
                <button @click="nextBook(true)">YES</button>
                <button @click="nextBook(false)">NO</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Book",
    beforeMount() {
        this.getName();
    },
    methods: {
        async getName() {
            const res = await fetch(
                "https://www.googleapis.com/books/v1/volumes?q=" + this.category
            );
            const data = await res.json();
            this.data = data.items.map((v) => {
                return {
                    id: v.id,
                    name: v.volumeInfo.title,
                    picture: v.volumeInfo.imageLinks.thumbnail,
                    isSaved: false,
                };
            });
            this.loaded = true;
        },
        nextBook(isYes) {
            if (isYes) {
                this.saved.push(this.data[this.currentElement]);
            }
            this.currentElement++;
            if (this.currentElement == this.data.length) {
                this.data = [];
                this.currentElement = 0;
            }
        },
    },
    data() {
        return {
            currentElement: 0,
            loaded: false,
            category: "cooking",
            data: [],
        };
    },
    props: {
        msg: String,
        saved: Array,
    },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    margin: 40px 0 0;
}
ul {
    list-style-type: none;
    padding: 0;
}
li {
    display: inline-block;
    margin: 0 10px;
}
a {
    color: #42b983;
}
.book {
    height: 250px;
}
</style>
