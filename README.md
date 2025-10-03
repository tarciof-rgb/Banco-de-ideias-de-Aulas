import { useState } from "react";

export default function BancoDeIdeias() {
  const [ideias, setIdeias] = useState([
    { materia: "Matemática", titulo: "Geometria com dobraduras" },
    { materia: "História", titulo: "Linha do tempo interativa" },
  ]);

  const [novaMateria, setNovaMateria] = useState("");
  const [novoTitulo, setNovoTitulo] = useState("");
  const [filtro, setFiltro] = useState("");

  const adicionarIdeia = (e) => {
    e.preventDefault();
    if (novaMateria && novoTitulo) {
      setIdeias([...ideias, { materia: novaMateria, titulo: novoTitulo }]);
      setNovaMateria("");
      setNovoTitulo("");
    }
  };

  const ideiasFiltradas = ideias.filter((ideia) =>
    filtro ? ideia.materia.toLowerCase().includes(filtro.toLowerCase()) : true
  );

  return (
    <div className="min-h-screen bg-gray-100 p-6 flex flex-col items-center">
      <h1 className="text-3xl font-bold mb-6">Banco de Ideias de Aulas</h1>

      {/* Formulário */}
      <form
        onSubmit={adicionarIdeia}
        className="bg-white shadow-md rounded-2xl p-6 mb-6 w-full max-w-lg"
      >
        <h2 className="text-xl font-semibold mb-4">Adicionar Ideia</h2>
        <input
          type="text"
          placeholder="Matéria"
          value={novaMateria}
          onChange={(e) => setNovaMateria(e.target.value)}
          className="w-full p-2 border rounded mb-3"
        />
        <input
          type="text"
          placeholder="Título da ideia"
          value={novoTitulo}
          onChange={(e) => setNovoTitulo(e.target.value)}
          className="w-full p-2 border rounded mb-3"
        />
        <button
          type="submit"
          className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition"
        >
          Salvar
        </button>
      </form>

      {/* Filtro */}
      <div className="mb-4 w-full max-w-lg">
        <input
          type="text"
          placeholder="Filtrar por matéria..."
          value={filtro}
          onChange={(e) => setFiltro(e.target.value)}
          className="w-full p-2 border rounded"
        />
      </div>

      {/* Lista de ideias */}
      <div className="w-full max-w-lg space-y-3">
        {ideiasFiltradas.map((ideia, index) => (
          <div
            key={index}
            className="bg-white shadow rounded-xl p-4 flex justify-between items-center"
          >
            <div>
              <h3 className="font-bold">{ideia.titulo}</h3>
              <p className="text-sm text-gray-600">{ideia.materia}</p>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}
