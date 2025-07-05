# Crear el archivo HTML completo con los 5 cuatrimestres de la Tecnicatura en Administración

html_content_full = """

<!DOCTYPE html>

<html lang="es">

<head>

  <meta charset="UTF-8" />

  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <title>Malla Curricular - Tecnicatura en Administración</title>

  <style>

    body { font-family: Arial, sans-serif; background: #f9f9f9; margin: 20px; }

    h1, h2 { text-align: center; }

    .info-header { text-align: center; margin-bottom: 30px; }

    .cuatrimestre { margin-bottom: 20px; }

    .cuatrimestre h3 { text-align: center; margin-bottom: 10px; }

    .materias { display: flex; flex-wrap: wrap; justify-content: center; gap: 8px; }

    .materia {

      padding: 8px 12px; background: #e0e0e0; border: 1px solid #ccc;

      border-radius: 6px; cursor: pointer; user-select: none;

    }

    .materia.aprobada { background: #a0d8a0; border-color: #5fa85f; }

    .materia.disabled { background: #f0f0f0; color: #999; border-color: #ccc; cursor: not-allowed; }

    .contador { text-align: center; font-size: 1.2em; margin-top: 20px; }

  </style>

</head>

<body>

  <div class="info-header">

    <h1>Tecnicatura Superior en Administración</h1>

    <h2>Plan 2024</h2>

    <p>Seleccioná las materias aprobadas para habilitar sus correlativas.</p>

  </div>



  <div class="cuatrimestre">

    <h3>1º Cuatrimestre</h3>

    <div class="materias">

      <div class="materia" id="1">Inglés I</div>

      <div class="materia" id="2">Administración General</div>

      <div class="materia" id="3">TIC I</div>

      <div class="materia" id="4">Matemática Aplicada</div>

    </div>

  </div>



  <div class="cuatrimestre">

    <h3>2º Cuatrimestre</h3>

    <div class="materias">

      <div class="materia" id="5" data-correlativas="3">TIC II</div>

      <div class="materia" id="6" data-correlativas="4">Estadística Aplicada</div>

      <div class="materia" id="7">Economía Argentina</div>

      <div class="materia" id="8">Sistemas Contables I</div>

    </div>

  </div>



  <div class="cuatrimestre">

    <h3>3º Cuatrimestre</h3>

    <div class="materias">

      <div class="materia" id="9" data-correlativas="1">Inglés II</div>

      <div class="materia" id="10" data-correlativas="2,7">Sistemas Administrativos</div>

      <div class="materia" id="11" data-correlativas="7,8">Régimen Tributario</div>

      <div class="materia" id="12" data-correlativas="1,2,5">Gestión Estratégica</div>

      <div class="materia" id="13" data-correlativas="5,8">Sistemas Contables II</div>

    </div>

  </div>



  <div class="cuatrimestre">

    <h3>4º Cuatrimestre</h3>

    <div class="materias">

      <div class="materia" id="14" data-correlativas="10,13">Recursos Humanos</div>

      <div class="materia" id="15" data-correlativas="6,10">Administración de Operaciones</div>

      <div class="materia" id="16" data-correlativas="6,10">Gestión Comercial</div>

      <div class="materia" id="17" data-correlativas="5,10">Inteligencia Artificial en Admin</div>

      <div class="materia" id="18" data-correlativas="1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17">Práctica Prof I</div>

    </div>

  </div>



  <div class="cuatrimestre">

    <h3>5º Cuatrimestre</h3>

    <div class="materias">

      <div class="materia" id="19" data-correlativas="11">Derecho Laboral</div>

      <div class="materia" id="20" data-correlativas="7,16">Marketing Digital</div>

      <div class="materia" id="21" data-correlativas="15,16,17">Administración Financiera</div>

      <div class="materia" id="22" data-correlativas="1,11,17">Innovación y Ambiente</div>

      <div class="materia" id="23" data-correlativas="18,19,20,21,22">Práctica Prof II</div>

    </div>

  </div>



  <div class="contador" id="contador">Materias aprobadas: 0</div>



  <script>

    const materias = document.querySelectorAll('.materia');

    const contador = document.getElementById('contador');



    function actualizarContador() {

      const aprobadas = document.querySelectorAll('.materia.aprobada').length;

      contador.textContent = `Materias aprobadas: ${aprobadas}`;

    }



    function actualizarCorrelativas() {

      materias.forEach(m => {

        const reqs = m.dataset.correlativas;

        if (reqs) {

          const ids = reqs.split(',');

          const habilitada = ids.every(id => document.getElementById(id).classList.contains('aprobada'));

          if (habilitada) {

            m.classList.remove('disabled');

          } else {

            m.classList.add('disabled');

          }

        }

      });

    }



    materias.forEach(m => {

      m.addEventListener('click', () => {

        if (m.classList.contains('disabled')) return;

        m.classList.toggle('aprobada');

        actualizarContador();

        actualizarCorrelativas();

      });

    });



    actualizarContador();

    actualizarCorrelativas();

  </script>

</body>

</html>

"""



from pathlib import Path

output_path = Path("/mnt/data/malla_curricular_admin_2024_full.html")

output_path.write_text(html_content_full, encoding="utf-8")

output_path.name
