<template>
  <div>
    <AddMember />
    <section>
      <h1>Directory</h1>
      <table>
        <tr>
          <th>Name</th>
          <th>Phone</th>
          <th id="remove">Remove</th>
        </tr>
        <tr v-if="name.length > 0 || phone.length > 0">
          <td>{{ name }}</td>
          <td>{{ phone }}</td>
        </tr>
        <tr v-for="(member, index) in members" :key="member.phone">
          <td>{{ member.name }}</td>
          <td>{{ member.phone }}</td>
          <td v-if="member.dateAdded" class="remove" @click="deleteMember({ member, index })">╳</td>
        </tr>
      </table>
    </section>
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import AddMember from "./AddMember";

export default {
  components: {
    AddMember
  },
  computed: mapState(["members", "name", "phone"]),
  methods: mapActions(["deleteMember"])
};
</script>

<style scoped>
table {
  margin-top: 2rem;
  width: 100%;
  color: rgb(128, 128, 128);
  border-collapse: collapse;
  cursor: default;
}
th,
td,
tr {
  text-transform: capitalize;
  padding: 0.65rem;
  text-align: left;
  font-size: 1.5rem;
  border: 1.5px solid rgb(128, 128, 128, 0.5);
}
th {
  padding: 0.3rem 0.65rem;
  font-size: 0.9rem;
  letter-spacing: 0.5px;
}
th:after {
  content: ":";
}
tr:hover :not(th) {
  color: white;
  background: rgba(40, 40, 40, 0.65);
}
#remove {
  width: 0;
}
.remove {
  text-align: center;
  cursor: pointer;
}
.remove:hover {
  color: rgb(255, 80, 78);
}
</style>
