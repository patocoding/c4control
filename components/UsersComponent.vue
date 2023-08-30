<template>
    <!-- <div>
        <div class="uQxNj" v-if="user">
            <p>{{ errorMsg }}</p>
        <input v-model="searchText" placeholder="Pesquisar por nome" class="p-2 mb-4 border rounded" />
        <div v-if="profiles.length > 0">
            <div>
                <h3 class="mb-5">Nome de Usuários</h3>
            <p v-for="profile in profiles" class="mb-4" :key="profile.id">{{ profile.full_name }} - <span class="font-bold">ID {{ profile.id }}</span> - Situação da Matricula: {{ profile.isMatriculaActive === true ?'Ativa' : 'Não Ativo'  }}</p>
            </div>
            <div>
                
            </div>
        </div>
        
        <p v-else>Nenhum perfil encontrado.</p>
        </div>
        
    </div> -->
    <div class="relative z-10 max-w-screen-sm">
      <p v-if="user" class="fVeafc in">Olá {{ user.user_metadata.full_name }}</p>
      <p v-else class="fVeafc">unauthenticated</p>
      
      <input v-model="searchText" placeholder="Pesquisar por nome" class="p-2 mb-4 border rounded" />
      <!-- <div v-if="profiles.length > 0">
            <div>
                <h3 class="mb-5">Nome de Usuários</h3>
            <p v-for="profile in profiles" class="mb-4" :key="profile.id">{{ profile.full_name }} - <span class="font-bold">ID {{ profile.id }}</span> - Situação da Matricula: {{ profile.isMatriculaActive === true ?'Ativa' : 'Não Ativo'  }}</p>
            </div>
            <div>
                
            </div>
        </div> -->
        <div v-if="filteredProfiles.length > 0">
  <div>
    <h3 class="mb-5">Nome de Usuários</h3>
    <p v-for="profile in filteredProfiles" class="mb-4" :key="profile.id">
      {{ profile.full_name }} - <span class="font-bold">ID {{ profile.id }}</span> -
      Situação da Matricula: {{ profile.isMatriculaActive === true ? 'Ativa' : 'Não Ativo' }}
    </p>
  </div>
</div>
        
        <p v-else>Nenhum perfil encontrado.</p>
        </div>
</template>

<script>
export default {
    name: 'UsersComponent',
    setup () {
        const profiles = ref([]); 
        const errorMsg = ref(null)
        const supabase = useSupabaseClient()
        const user = useSupabaseUser()
        const searchText = ref('');

        const getUsers = async () => {
            const { data, error } = await supabase
            .from('profiles')
            .select('*');

            if (data) {
                profiles.value = data; // Armazena todos os perfis no array 'profiles'
                console.log('foi');
            }
            
            if (error) {
                errorMsg.value = error.message;
            }
        }

        const filteredProfiles = computed(() => {
  if (!searchText.value) {
    return profiles.value;
  }
  const lowerSearchText = searchText.value.toLowerCase();
  return profiles.value.filter(profile =>
    profile.full_name && profile.full_name.toLowerCase().includes(lowerSearchText)
  );
});

        

        getUsers();

        return { profiles, errorMsg , user, searchText, filteredProfiles,};
    }
}

  

</script>

<style scoped>

</style>