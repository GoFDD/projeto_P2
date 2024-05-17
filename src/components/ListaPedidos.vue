<template>
  <main>
    <div class="container-fluid">
      <div class="row">
        <h2 class="my-4">Listagem de Pedidos</h2>
        <hr>
        <form class="d-flex justify-content-end align-items-center mb-3">
          <div class="input-group pesquisa me-2">
            <input type="text" class="form-control" placeholder="Digite sua pesquisa aqui" aria-label="Pesquisa" aria-describedby="button-addon2" v-model="consultaBusca">
            <button class="btn btn-primary" type="button" id="button-addon2">Pesquisar</button>
          </div>
          <div class="btn-group">
            <button type="button" class="btn btn-secondary dropdown-toggle" data-bs-toggle="dropdown" aria-expanded="false">
              Linhas
            </button>
            <ul class="dropdown-menu">
              <li v-for="opcao in opcoesLinhas" :key="opcao">
                <a class="dropdown-item" href="#" @click="setLinhasPorPagina(opcao)">{{ opcao }} linhas</a>
              </li>
            </ul>
          </div>
        </form>
        <div class="table-responsive">
          <table class="table table-striped table-bordered tabela-pedido">
            <thead class="cara">
              <tr class="teste">
                <th colspan="7" class="text-center">Painel de Pedidos</th>
              </tr>
              <tr>
                <th scope="col" class="py-3 px-2 text-lg">Código</th>
                <th scope="col" class="py-3 px-4 text-lg">Cliente</th>
                <th scope="col" class="py-3 px-4 text-lg">Qtd</th>
                <th scope="col" class="py-3 px-4 text-lg">Valor</th>
                <th scope="col" class="py-3 px-4 text-lg">Status</th>
                <th scope="col" class="py-3 px-4 text-lg">Método</th>
                <th scope="col" class="py-3 px-4 text-lg">Ações</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(pedido, index) in pedidosPaginados" :key="pedido.id">
                <td>{{ index + 1 }}</td>
                <td>{{ pedido.cliente }}</td>
                <td>{{ pedido.qtd }}</td>
                <td>{{ pedido.valorTotal }}</td>
                <td>
                  <span :class="{'badge bg-success': pedido.status === 'Aprovado', 'badge bg-danger': pedido.status === 'Rejeitado', 'badge bg-warning': pedido.status === 'Pendente', 'badge bg-info': pedido.status === 'Em andamento'}">{{ pedido.status }}</span>
                </td>
                <td>{{ pedido.metodo }}</td>
                <td>
                  <button class="btn btn-sm btn-info me-2"><i class="fas fa-edit"></i> Editar</button>
                  <button class="btn btn-sm btn-danger"><i class="fas fa-trash-alt"></i> Excluir</button>
                </td>
              </tr>
              <tr v-if="pedidosPaginados.length === 0">
                <td colspan="7" class="text-center">Nenhum pedido encontrado.</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <nav aria-label="Navegação de página exemplo">
        <ul class="pagination justify-content-center">
          <li class="page-item disabled">
            <a class="page-link" href="#" tabindex="-1">Anterior</a>
          </li>
          <li class="page-item"><a class="page-link" href="#">1</a></li>
          <li class="page-item"><a class="page-link" href="#">2</a></li>
          <li class="page-item"><a class="page-link" href="#">3</a></li>
          <li class="page-item">
            <a class="page-link" href="#">Próximo</a>
          </li>
        </ul>
      </nav>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      pedidos: [
        { id: 1, cliente: 'João Silva', dataPedido: '2024-05-12', qtd: 5, valorTotal: 100.50, status: 'Aprovado', metodo: 'Pagseguro' },
        { id: 2, cliente: 'Maria Oliveira', dataPedido: '2024-05-11', qtd: 5, valorTotal: 75.25, status: 'Pendente', metodo: 'PayPal' },
        { id: 3, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento', metodo: 'Cartão de Crédito' },
        { id: 4, cliente: 'João Silva', dataPedido: '2024-05-12', qtd: 5, valorTotal: 100.50, status: 'Aprovado', metodo: 'Pagseguro' },
        { id: 5, cliente: 'Maria Oliveira', dataPedido: '2024-05-11', qtd: 5, valorTotal: 75.25, status: 'Pendente', metodo: 'PayPal' },
        { id: 6, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento', metodo: 'Cartão de Crédito' },
        { id: 7, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento', metodo: 'Cartão de Crédito' },
        { id: 8, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento', metodo: 'Cartão de Crédito' },
        { id: 9, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento', metodo: 'Cartão de Crédito' },
        { id: 10, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento', metodo: 'Cartão de Crédito' },
      ],
      consultaBusca: '',
      linhasPorPagina: 5,
      opcoesLinhas: [5, 10, 15, 20]
    };
  },
  computed: {
    pedidosFiltrados() {
      return this.pedidos.filter(pedido =>
        pedido.cliente.toLowerCase().includes(this.consultaBusca.toLowerCase())
      );
    },
    pedidosPaginados() {
      return this.pedidosFiltrados.slice(0, this.linhasPorPagina);
    }
  },
  methods: {
    setLinhasPorPagina(opcao) {
      this.linhasPorPagina = opcao;
    }
  }
};
</script>

<style scoped>
th {
  color: #fff;
  background-color: #1E293B;
}
</style>
