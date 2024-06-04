<template>
    <div class="buscar-mascota">
        <h1>Busca una mascota en Mercado Libre</h1>
        <p>Recibe información de un tipo de mascota que venden en mercado libre.</p>
        <form @submit.prevent="realizarBusqueda">
            <div class="form-group">
                <label for="palabraClave">Palabra Clave</label>
                <input type="text" id="palabraClave" v-model="palabraClave" placeholder="Ingrese una palabra clave"
                    required />
            </div>
            <div class="form-group">
                <label for="correo">Correo Electrónico</label>
                <input type="email" id="correo" v-model="correo" placeholder="Ingrese su correo electrónico" required />
            </div>
            <div class="form-buttons">
                <button type="submit">Realizar Búsqueda</button>
                <button type="button" @click="revisarCola">Revisar Cola</button>
            </div>
        </form>
        <div class="image-container">
            <img src="https://caracoltv.brightspotcdn.com/dims4/default/91fc79f/2147483647/strip/false/crop/1280x720+0+0/resize/1200x675!/quality/90/?url=http%3A%2F%2Fcaracol-brightspot.s3.us-west-2.amazonaws.com%2F2f%2Fe5%2F845a68264ba4be6d5d57696a9b3e%2Fmercado-libre.jpg"
                alt="Imagen mercado libre">
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            palabraClave: '',
            correo: ''
        };
    },
    methods: {
        realizarBusqueda() {
            const data = {
                keyword: this.palabraClave,
                email: this.correo
            };

            axios.post('http://localhost:4000/add-to-queue', data)
                .then(response => {
                    console.log('Datos enviados correctamente:', data);
                    console.log('Respuesta del servidor:', response.data);
                    alert(`Búsqueda realizada con éxito. Palabra clave: ${this.palabraClave}, Correo electrónico: ${this.correo}`);
                    // Limpiar campos de entrada
                    this.palabraClave = '';
                    this.correo = '';
                })
                .catch(error => {
                    console.error('Error al realizar la búsqueda:', error);
                    alert(`Error al realizar la búsqueda: ${error.message}`);
                });

        },
        revisarCola() {
            alert('Revisando la cola de búsquedas...');
        }
    }
};
</script>

<style scoped>
.buscar-mascota {
    max-width: 700px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
    font-size: 24px;
    text-align: center;
    margin-bottom: 10px;
}

p {
    font-size: 14px;
    text-align: center;
    margin-bottom: 20px;
}

.form-group {
    display: flex;
    align-items: center;
    margin-bottom: 15px;
}

label {
    width: 20%;
    margin-right: 10px;
    text-align: right;
    font-size: 14px;
}

input[type="text"],
input[type="email"] {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

.form-buttons {
    display: flex;
    justify-content: space-between;
    padding: 5%;
}

button {
    padding: 15px 20px;
    border: none;
    border-radius: 5px;
    background-color: #007bff;
    color: white;
    cursor: pointer;
    transition: background-color 0.3s ease;
    font-size: 14px;
}

button:hover {
    background-color: #0056b3;
}

button[type="button"] {
    background-color: #28a745;
}

button[type="button"]:hover {
    background-color: #218838;
}

.image-container {
    display: flex;
    justify-content: center;
    margin-top: 20px;
}

.image-container img {
    max-width: 200px;
    height: auto;
    border-radius: 10px;
}
</style>