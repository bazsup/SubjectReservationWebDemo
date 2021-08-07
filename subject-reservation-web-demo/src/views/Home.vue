<template>
  <div class="home">
    <br />
    <p style="font-family: Roboto; font-size: 18pt">
      SIT Subject Reservation Web >>>> list-subjects
    </p>
    <br />
    <v-row justify="center" align="top" no-gutters style="height: 150px">
      <v-col v-for="subject in subjectList" :key="subject.subjectId" cols="3" class="pa-2">
        <subject :subject="subject" @fetchSubjects="getSubjectList()" @subjectIsMax="errorSubjectIsMax()" />
      </v-col>
    </v-row>
    <v-dialog v-model="isError" width="500">

      <v-card>
        <v-card-title class="text-h5 grey lighten-2">
          Notification from Ajarn
        </v-card-title>
        <v-card-text>
          อาจารย์ซึ้งใจเป็นอย่างมากที่ทุกคนตั้งใจกันอยากเรียนแต่วิชาเต็มแล้ว TwT
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="isError = false"> ยอมรับน้ำตาไหล </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>


<script>
import Subject from "../components/Subject";
import { fetchSubjectList } from "../service/subject";
export default {
  name: "Home",
  components: {
    Subject,
  },
  data: () => ({
    alignments: ["start", "center", "end"],
    subjectList: [
      {
        subjectId: "int101",
        quota: 30,
        currentStudentNumber: 0,
        subjectName: "Introduction to Java 1",
      },
    ],
    isError: false,
  }),
  mounted() {
    this.getSubjectList();
  },
  methods: {
    getSubjectList: async function () {
      try {
        this.subjectList = await fetchSubjectList();
        this.subjectList.forEach(subject => {
          subject.image = 'https://quarkus.io/assets/images/quarkus_card.png'
        });
      } catch (error) {
        console.log(error.message);
      }
    },
    errorSubjectIsMax: function(){
        this.isError = true;
    }
  },
};
</script>
