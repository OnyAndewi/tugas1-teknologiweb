<template>
 <nav id="header" class="w-full  top-10 py-1 bg-white shadow-lg border-b border-blue-400">
        <div class="w-full flex items-center justify-between mt-0 px-6 py-2">
            <label for="menu-toggle" class="cursor-pointer md:hidden block">
                      <svg class="fill-current text-blue-600" xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 20 20">
                         <title>menu</title>
                         <path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"></path>
                      </svg>
                   </label>
            <input class="hidden" type="checkbox" id="menu-toggle">

            <div class="hidden md:flex md:items-center md:w-auto w-full order-3 md:order-1" id="menu">
                <nav>
                    <ul class="md:flex items-center justify-between text-base text-blue-600 pt-4 md:pt-0">
                        <li><a class="inline-block no-underline hover:text-black font-medium text-lg py-2 px-4 lg:-ml-2" href="#">Home</a></li>
                        <li><a class="inline-block no-underline hover:text-black font-medium text-lg py-2 px-4 lg:-ml-2" href="#">Setting</a></li>
                        <li><a class="inline-block no-underline hover:text-black font-medium text-lg py-2 px-4 lg:-ml-2" href="#">About</a></li>
                    </ul>
                </nav>
            </div>

            <div class="order-2 md:order-3 flex flex-wrap items-center justify-end mr-0 md:mr-4" id="nav-content">
                <div class="auth flex items-center w-full md:w-full">
                    <button class="bg-yellow-200 text-gray-800  p-2 rounded border-gray-300 mr-4 hover:bg-gray-100 hover:text-gray-700">Sign in</button>
                    <button class="bg-blue-200 text-gray-800  p-2 rounded border border-gray-100 hover:bg-gray-100 hover:text-gray-700">Sign up</button>
                </div>
            </div>
        </div>
    </nav>
    <div id="app">
        <!-- Container -->
        <div class="container mx-auto">
            <div class="flex justify-center px-6 my-12">
                <!-- Row -->
                <div class="w-full xl:w-3/4 lg:w-13/15 flex">
                    <!-- Col -->
                    <div class="w-full h-auto p-6 border border-blue-200  hidden lg:block lg:w-8/12 bg-cover rounded-l-lg">
                        <h3 class="pt-4 text-2xl text-center">Biodata PNS</h3>
                        <form v-on:submit.prevent="TambahDataPegawai" class="p-4 bg-white rounded">
                            <div class="grid grid-cols-4 gap-4 p-2">
                                <div class="md:col-span-1 col-span-4">NIP</div>
                                <div class="md:col-span-3 col-span-4">
                                    <input type="text" v-model="inputP.nip_pegawai" class="border border-blue-400 rounded">
                                </div>
                            </div>
                            <div class="grid grid-cols-4 gap-4 p-2">
                                <div class="md:col-span-1 col-span-4">Nama Pegawai</div>
                                <div class="md:col-span-3 col-span-4">
                                    <input type="text" v-model="inputP.nama_pegawai" class="border border-blue-400 rounded">
                                </div>
                            </div>
                            <div class="grid grid-cols-4 gap-4 p-2">
                                <div class="md:col-span-1 col-span-4">Jenis Kelamin</div>
                                <div class="md:col-span-3 col-span-4">
                                    <select v-model="inputP.jenis_kelamin" class="border border-blue-400 rounded" id="">
                                        <option v-for="item in items" :value="item.id" :key="item.id">
                                                {{item.type}}
                                        </option>
                                    </select>
                                </div>
                            </div>
                            <div class="grid grid-cols-4 gap-4 p-2">
                                <div class="md:col-span-1 col-span-4">Usia Pegawai</div>
                                <div class="md:col-span-3 col-span-4">
                                    <input type="number" v-model="inputP.usia_pegawai" class="border border-blue-400 rounded">
                                </div>
                            </div>
                            <div class="grid grid-cols-4 gap-4 p-2">
                                <div class="md:col-span-1 col-span-4">Alamat Pegawai</div>
                                <div class="md:col-span-3 col-span-4">
                                    <input type="text" v-model="inputP.alamat_pegawai" class="border border-blue-400 rounded">
                                </div>
                            </div>
                            <div class="grid grid-cols-4 gap-4 p-2">
                                <button class="py-2 px-2 text-white rounded-lg bg-red-500 shadow-lg block md:inline-block">Save</button>
                            </div>
                            <div class="grid grid-cols-4 gap-4 p-2">
                                {{ message }}
                            </div>
                        </form>
                    </div>
                    <!-- Col -->
                    <div class="w-full lg:w-13/12 bg-white p-5 rounded-lg lg:rounded-l-none bg-blue-100">
                        <h3 class="pt-4 text-2xl text-center">List Biodata</h3>
                        <table class="w-full">
                            <thead>
                                <tr class="text-s font-semibold tracking-wide text-left text-blue-900 bg-yellow-100 uppercase border-b border-gray-600">
                                    <th align=center>Nip Pegawai</th>
                                    <th align=center>Nama Pegawai</th>
                                    <th align=center>Status Pegawai</th>
                                    <th align=center>Usia Pegawai</th>
                                    <th align=center>Alamat Pegawai</th>
                                    <th align=center>Aksi</th>
                                </tr>
                            </thead>
                            <tbody> 
                                <tr v-for="(item, index) in Setting" :key="index" class="text-gray-700">
                                    <td class="px-4 py-3 border">
                                        {{ item.nip_pegawai }}
                                    </td> 
                                    <td class="px-4 py-3 border">
                                        {{ item.nama_pegawai }}
                                    </td>
                                    <td class="px-4 py-3 border">
                                        {{getType(item.jenis_kelamin)}}
                                    </td>
                                    <td class="px-4 py-3 border">
                                        {{ item.usia_pegawai }}
                                    </td>
                                    <td class="px-4 py-3 border">
                                        {{ item.alamat_pegawai }}
                                    </td>
                                    <td class="px-4 py-3 border">
                                        <button class="bg-red-400 py-1 px-2 rounded-lg text-white" v-on:click="Setting.splice(index, 1)">Remove</button>||
                                        <button class="bg-yellow-400 py-1 px-2 rounded-lg text-white" v-on:click="editProduct(index, item)">Edit</button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
  nama_pegawai: 'App',
  components: {
  },
  data() {
    return {
      inputP: {},
            message: '',
            items: [{
                id: 1,
                type: 'Laki-laki'
            }, {
                id: 2,
                type: 'Perempuan'
            }],
            Setting: [],
            productID: 1,
            ind: null
    }
  },
  methods: {
    TambahDataPegawai: function() {
                if (this.ind != null) {
                    Object.assign(this.Setting[this.ind], {
                        nip_pegawai: this.inputP.nip_pegawai,
                        nama_pegawai: this.inputP.nama_pegawai,
                        jenis_kelamin: this.inputP.jenis_kelamin,
                        usia_pegawai: this.inputP.usia_pegawai,
                        alamat_pegawai: this.inputP.alamat_pegawai
                    })
                } else {
                    this.Setting.push({
                        nip_pegawai: this.inputP.nip_pegawai,
                        nama_pegawai: this.inputP.nama_pegawai,
                        jenis_kelamin: this.inputP.jenis_kelamin,
                        usia_pegawai: this.inputP.usia_pegawai,
                        alamat_pegawai: this.inputP.alamat_pegawai
                    })
                }
                this.inputP.nip_pegawai = "";
                this.inputP.nama_pegawai = "";
                this.inputP.jenis_kelamin = "";
                this.inputP.usia_pegawai = "";
                this.inputP.alamat_pegawai = "";
                this.ind = null;
            },
            editProduct: function(ind, p) {
                this.ind = ind;
                this.inputP.nip_pegawai = p.nip_pegawai;
                this.inputP.nama_pegawai = p.nama_pegawai;
                this.inputP.jenis_kelamin = p.jenis_kelamin;
                this.inputP.usia_pegawai = p.usia_pegawai;
                this.inputP.usia_pegawai = p.alamat_pegawai;
            },
            getType: function(id) {
                // var m = this.items.filter(function(item) {
                //     return item.id.match(id)
                // });
                var m = this.items.filter(function(elem) {
                    if (elem.id == id) return elem;
                });
                return m[0].type;

            }
  }
}
</script>