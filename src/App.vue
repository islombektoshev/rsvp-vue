<template>
  <div class="App" id="app">
    <header>
      <h1>RSVP</h1>
      <p>A Treehouse App</p>
      <input type="text" v-model="searchText" placeholder="Search">
      <form @submit.prevent="add">
        <input type="text" value="Safia" placeholder="Invite Someone" v-model="name">
        <button type="submit" name="submit" value="submit">Submit</button>
      </form>
    </header>
    <div class="main">
      <div>
        <h2>Invitees</h2>
        <label>
          <input type="checkbox" v-model="hideDontResponded"> Hide those who haven't responded
        </label>
      </div>
      <Stats
              :total="this.people.length"
              :un-confirmed="getUnConfirmedCount"
      ></Stats>
      <ul>
        <li class="pending" v-if="name.length>0"><span>{{name}}</span></li>
        <Card v-for="(item, index) in getPeople()"
              :key="index"
              :person="item"
              :is-confirmed="item.isConfirmed"
              @changeName="updateName"
        >
          {{item}}
        </Card>
      </ul>
    </div>
  </div>
</template>

<script>
    import Stats from "./components/Stats";
    import Card from "./components/Card";

    export default {
        name: 'App',
        // eslint-disable-next-line vue/no-unused-components
        components: {Card, Stats},
        data: function () {
            return {
                name: "",
                hideDontResponded: false,
                searchText: "",
                people: [
                    {name: "Islom", isConfirmed: true}
                ]
            };
        },
        methods: {
            add() {
                console.error('debug');
                let d = {name: this.name, isConfirmed: false};
                this.people.unshift(d);
                this.name = "";
            },
            updateName(name, index) {
                this.people[index].name = name;
            },
            getPeople() {
                let result = this.people.filter(p => {
                    // agar search text bo'sh bo'lsa va not confirmed personlarni
                    // ko'rsatmaslik kerak bo'lmasa barchasini o'tkazib yuboramiz
                    let noSearch = this.searchText.length === 0;
                    if ((noSearch && !this.hideDontResponded)
                        || (noSearch && this.hideDontResponded && p.isConfirmed)) return true;

                    // o'xshash isimligni aniqlab olamiz agar oxshash bo'sa `true`
                    let isSameName = p.name.toUpperCase().trim().startsWith(this.searchText.toUpperCase().trim());

                    // agar o'xsass isim bo'lsa va confirmed personlarni
                    // ko'rsatmaslik kerak bo'lmasa faqat oxshashligiga qaytaradi
                    // aks holda faqat person confirmation qilganigaham qaraladni
                    return (isSameName && !this.hideDontResponded)
                            || (isSameName && this.hideDontResponded && p.isConfirmed);
                });
                return result
            }

        },
        computed: {
            getUnConfirmedCount() {
                let count = 0;
                this.people.forEach(p => {
                    if (!p.isConfirmed) count++;
                });
                return count;
            },

        }
    }
</script>

<style>

</style>
