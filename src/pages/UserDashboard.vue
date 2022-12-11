<template>
    <q-header class="transparent text-white">
      <q-toolbar >
        <ClassroomToggle/>
        <q-toolbar-title></q-toolbar-title>
        <q-btn flat round dense icon="emoji_events" class="q-mr-sm" to="/user-achievements"/>
        <q-btn flat round dense icon="settings" class="q-mr-sm"  to="/settings"/>
      </q-toolbar>
    </q-header>
    <q-page class="flex justify-center items-end full-height full-width text-center">
        <q-container class="relative text-center mb-n12">
            <v-sheet color="transparent">
                <v-progress-linear 
                    color="white"
                    :model-value="user.active.data.profile?.level.percentage" 
                    :height="20" 
                    rounded="lg"
                ></v-progress-linear>
                <v-container class="pt-2 pb-2 text-white">
                    <v-row>
                        <v-col cols="6" class="pl-0 pr-0 text-left">
                            <b>Level {{user.active.data.profile?.level.id}}</b>
                        </v-col>
                        <v-col cols="6" class="pl-0 pr-0 text-right">
                            <b>{{user.active.data.profile?.total_points}}/{{user.active.data.profile?.level.points_to}}</b>
                        </v-col>
                    </v-row>
                </v-container>
            </v-sheet>
            <v-img
                class="ma-auto"
                width="170"
                :src="`${CONFIG.API_HOST}/images/dershane/hero_${user.active.data.profile?.hero}_hello.png`"
            >
            </v-img>
        </q-container>
        <q-card color="white" class="relative text-center pl-2 pr-2 pt-6 pb-6 rounded-t-xl">
            <h2>{{user.active.data.name}}</h2>
            <v-card class="mt-4 mb-4 text-left"  rounded="lg">
                <v-row align="center" no-gutters class="pa-2">
                    <v-col cols="2">
                        <v-avatar color="grey-lighten-1">
                            <v-img :src="`${CONFIG.API_HOST}${classroom.active?.introimage}`" cover></v-img>
                        </v-avatar>
                    </v-col>
                    <v-col class="text-left" cols="8">
                        <h4>{{classroom.active?.title}}</h4>
                        <p class="text-grey">
                            Current classroom
                        </p>
                    </v-col>
                    <v-col class="text-medium-emphasis text-truncate" cols="2">
                        <v-btn icon="mdi-account-convert-outline" to="/user-startup" variant="text"></v-btn>
                    </v-col>
                </v-row>
            </v-card>
            <v-btn
                block
                rounded="lg"
                to="user-edit"
                append-icon="mdi-account-edit"
            >
                <label>Edit profile</label>
            </v-btn>
            <v-container class="mt-4 mb-4 pa-0">
                <v-row >
                    <v-col cols="6">
                        <v-card class="pa-2 pv-2 text-left" rounded="lg">
                            <h3>{{user.active.data.profile?.total_exercises}}</h3>
                            <p class="text-grey">Exercises</p>
                            <v-tooltip activator="parent" location="top">
                                Total exercises that you have done
                            </v-tooltip>
                        </v-card>
                    </v-col>
                    <v-col cols="6">
                        <v-card class="pa-2 text-left" rounded="lg">
                            <h3>{{user.active.data.profile?.total_points}}</h3>
                            <p class="text-grey">Points</p>
                            <v-tooltip activator="parent" location="top">
                                Total points that you have scored
                            </v-tooltip>
                        </v-card>
                    </v-col>
                    <v-col cols="6">
                        <v-card class="pa-2 text-left" rounded="lg">
                            <h3>{{user.active.data.profile?.total_classrooms}}</h3>
                            <p class="text-grey">Classrooms</p>
                            <v-tooltip activator="parent" location="top">
                                Total classrooms that you are member of
                            </v-tooltip>
                        </v-card>
                    </v-col>
                    <v-col cols="6">
                        <v-card class="pa-2 text-left" rounded="lg">
                            <h3>{{user.active.data.profile?.total_achievements}}</h3>
                            <p class="text-grey">Achievements</p>
                            <v-tooltip activator="parent" location="top">
                                Total achievements that you have gained
                            </v-tooltip>
                        </v-card>
                    </v-col>
                </v-row>
            </v-container>
            <v-btn
                block
                rounded="lg"
                color="primary"
                @click="exitUser(); "
                append-icon="mdi-logout-variant"
            >
                <label>Sign out</label>
            </v-btn>
        </q-card>
    </q-page>
</template>

<script setup>
import { useUserStore } from '../stores/user'
import { useClassroom } from '../composables/useClassroom'
import { useRouter } from 'vue-router'
import ClassroomToggle from '../components/ClassroomToggle.vue'
import { CONFIG } from '../config.js'
import { ref } from 'vue'

const { user, signOut } = useUserStore()
const { classroom } = useClassroom()
const router = useRouter()


const sheet = ref(false);


const exitUser = async function () {
    await signOut();
    return router.push('/user-startup');
}


</script>