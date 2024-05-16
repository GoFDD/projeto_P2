<template>
  <main>
    <div class="container-fluid">
      <div class="row">
        <h2 class="my-4">Cadastro de Pedido de Venda</h2>
        <hr>
        <form @submit.prevent="submitOrder" class="mb-4">
          <div class="row g-3">
            <div class="col-md-6">
              <label for="cliente" class="form-label">Cliente:</label>
              <input type="text" class="form-control" id="cliente" v-model="cliente" required>
            </div>
            <div class="col-md-6">
              <label for="produto" class="form-label">Produto:</label>
              <input type="text" class="form-control" id="produto" v-model="produto" required>
            </div>
            <div class="col-md-6">
              <label for="quantidade" class="form-label">Quantidade:</label>
              <input type="number" class="form-control" id="quantidade" v-model.number="quantidade" required>
            </div>
            <div class="col-md-6">
              <label for="preco" class="form-label">Preço:</label>
              <input type="number" class="form-control" id="preco" v-model.number="preco" required>
            </div>
          </div>
          <button type="submit" class="btn btn-primary mt-3">Cadastrar Pedido</button>
        </form>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      cliente: '',
      produto: '',
      quantidade: 0,
      preco: 0
    };
  },
  methods: {
    submitOrder() {
      // Aqui você pode enviar os dados do pedido para o backend e lidar com o armazenamento no banco de dados
      // Depois de enviar, você pode redirecionar o usuário de volta à página de listagem de pedidos
      // Exemplo de redirecionamento:
      // this.$router.push({ name: 'ListagemPedidos' });
      alert('Pedido cadastrado com sucesso!');
    }
  }
};
</script>

<style scoped>
/* Estilos específicos do componente aqui */
</style>
