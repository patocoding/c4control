<template>
    <div>   
        <div class="uQxNj" v-if="user">
            <div>
                <h1 class="kKxhrq">Usuários</h1>
            <users-component/>
            </div>
            
        </div>
        
    </div>
</template>


<script setup lang="ts">
const client = useSupabaseAuthClient()
const user = useSupabaseUser()
const loading = ref(false)
const router = useRouter()

useHead({
  title: 'users',
  meta: [
    { name: 'description', content: 'Authentication template with email and password, using Supabase. If you want to a quick start to your next Nuxt3 app, please feel free to use this template.' }
  ]
})
</script>

<style scoped>
    .pointer{
        cursor: pointer;
    }
</style>