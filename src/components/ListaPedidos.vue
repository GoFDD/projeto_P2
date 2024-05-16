<template>
  <main>
    <div class="container-fluid">
        <div class="row">
          <h2 class="my-4">Listagem de Pedidos</h2>
          <hr>
          <form class="d-flex justify-content-end">
            <div class="input-group mb-3 pesquisa ">
              <button class="btn btn-primary" type="button" id="button-addon2">Pesquisar</button>
              <input type="text" class="form-control" placeholder="Digite sua pesquisa aqui" aria-label="Pesquisa" aria-describedby="button-addon2" v-model="consultaBusca">
            </div>
          </form>
          <div class="table-responsive">
            <table class="table table-striped table-bordered tabela-pedido">
              <thead class="cara">
                <tr class="teste">
                  <th colspan="7" class="text-center">Cabeçalho Acima da Tabela</th>
                </tr>
                <tr>
                  <th scope="col" class="py-3 px-2 text-lg">Código</th>
                  <th scope="col" class="py-3 px-4 text-lg">Cliente</th>
                  <th scope="col" class="py-3 px-4 text-lg">Qtd</th>
                  <th scope="col" class="py-3 px-4 text-lg">Valor</th>
                  <th scope="col" class="py-3 px-4 text-lg">Status</th>
                  <th scope="col" class="py-3 px-4 text-lg">Método</th>
                  <th scope="col" class="py-3 px-4 text-lg">Alterar</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(pedido, index) in pedidosFiltrados" :key="pedido.id">
                  <td>{{ index + 1 }}</td>
                  <td>{{ pedido.cliente }}</td>
                  <td>{{ pedido.qtd }}</td>
                  <td>{{ pedido.valorTotal }}</td>
                  <td>
                    <span :class="{'badge bg-success': pedido.status === 'Aprovado', 'badge bg-danger': pedido.status === 'Rejeitado', 'badge bg-warning': pedido.status === 'Pendente', 'badge bg-info': pedido.status === 'Em andamento'}">{{ pedido.status }}</span>
                  </td>
                  <td>{{ pedido.metodo }}</td>
                  <td>
                    <button class="btn btn-sm btn-info"><i class="bi bi-pencil"></i> Editar</button>
                    <button class="btn btn-sm btn-danger"> Excluir</button>
                  </td>
                </tr>
                <tr v-if="pedidosFiltrados.length === 0">
                  <td colspan="6" class="text-center">Nenhum pedido encontrado.</td>
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
    </div> <!-- END-->
  </main>
</template>

<script>
export default {
  data() {
    return {
      pedidos: [
        { id: 1, cliente: 'João Silva', dataPedido: '2024-05-12', qtd: 5, valorTotal: 100.50, status: 'Aprovado', metodo: 'Pagseguro' },
        { id: 2, cliente: 'Maria Oliveira', dataPedido: '2024-05-11', qtd: 5, qtd: 5, valorTotal: 75.25, status: 'Pendente' },
        { id: 3, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento'  },
        { id: 4, cliente: 'João Silva', dataPedido: '2024-05-12', qtd: 5, valorTotal: 100.50, status: 'Aprovado' },
        { id: 5, cliente: 'Maria Oliveira', dataPedido: '2024-05-11', qtd: 5, valorTotal: 75.25, status: 'Pendente' },
        { id: 6, cliente: 'José Santos', dataPedido: '2024-05-10', qtd: 5, valorTotal: 120.75, status: 'Em andamento' },
        // Mais pedidos...
      ],
      consultaBusca: ''
    };
  },
  computed: {
    pedidosFiltrados() {
      return this.pedidos.filter(pedido =>
        (pedido.cliente && typeof pedido.cliente === 'string' && pedido.cliente.toLowerCase().includes(this.consultaBusca.toLowerCase()))
      );
    }
  },
  methods: {
    formatarData(data) {
      // Implemente a formatação da data conforme necessário
      return data;
    },
    formatarValor(valor) {
      // Implemente a formatação do valor conforme necessário
      return valor;
    }
  }
};
</script>

<style scoped>
th{
  color: #fff;
  background-color: #1E293B;
}
</style>
