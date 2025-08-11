<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PARAÍSO DAS MADEIRAS VZP - Materiais de Construção</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        /* Custom styles */
        .sticky-header {
            position: sticky;
            top: 0;
            z-index: 50;
        }
        .material-card {
            transition: transform 0.2s, box-shadow 0.2s;
        }
        .material-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .cart-item {
            animation: fadeIn 0.3s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .search-highlight {
            background-color: #fef08a;
        }
    </style>
</head>
<body class="bg-gray-50">
    <!-- Header -->
    <header class="sticky-header bg-green-800 text-white shadow-lg">
        <div class="container mx-auto px-4 py-4">
            <div class="flex flex-col md:flex-row justify-between items-center">
                <div class="flex items-center mb-4 md:mb-0">
                    <i class="fas fa-tree text-3xl mr-3"></i>
                    <h1 class="text-2xl md:text-3xl font-bold">PARAÍSO DAS MADEIRAS VZP</h1>
                </div>
                
                <div class="flex items-center space-x-4">
                    <div class="relative">
                        <input type="text" id="searchInput" placeholder="Buscar produto..." 
                               class="px-4 py-2 rounded-full border border-gray-300 focus:outline-none focus:ring-2 focus:ring-green-500 text-gray-800 w-full md:w-64">
                        <i class="fas fa-search absolute right-3 top-3 text-gray-400"></i>
                    </div>
                    
                    <button id="cartButton" class="relative">
                        <i class="fas fa-shopping-cart text-2xl"></i>
                        <span id="cartCount" class="absolute -top-2 -right-2 bg-yellow-500 text-white rounded-full w-6 h-6 flex items-center justify-center text-sm font-bold">0</span>
                    </button>
                </div>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-4 py-8">
        <!-- Categories -->
        <div class="mb-8">
            <h2 class="text-xl font-semibold mb-4 text-gray-800">Categorias</h2>
            <div class="flex flex-wrap gap-2">
                <button class="category-btn px-4 py-2 bg-green-100 text-green-800 rounded-full hover:bg-green-200 transition">Todos</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Madeiras</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Ferragens</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Hidráulica</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Elétrica</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Tintas</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Ferramentas</button>
                <button class="category-btn px-4 py-2 bg-gray-100 text-gray-800 rounded-full hover:bg-gray-200 transition">Churrasqueiras</button>
            </div>
        </div>

        <!-- Products Grid -->
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6" id="productsGrid">
            <!-- Products will be dynamically inserted here -->
        </div>
    </main>

    <!-- Shopping Cart Sidebar -->
    <div id="cartSidebar" class="fixed inset-y-0 right-0 w-full md:w-96 bg-white shadow-xl transform translate-x-full transition-transform duration-300 ease-in-out z-50 overflow-y-auto">
        <div class="p-6">
            <div class="flex justify-between items-center mb-6">
                <h2 class="text-xl font-bold text-gray-800">Carrinho de Compras</h2>
                <button id="closeCart" class="text-gray-500 hover:text-gray-700">
                    <i class="fas fa-times"></i>
                </button>
            </div>
            
            <div id="cartItems" class="mb-4">
                <!-- Cart items will be inserted here -->
                <p id="emptyCartMessage" class="text-gray-500 text-center py-8">Seu carrinho está vazio</p>
            </div>
            
            <div class="border-t border-gray-200 pt-4">
                <div class="flex justify-between mb-2">
                    <span class="font-medium">Subtotal:</span>
                    <span id="subtotal">R$ 0,00</span>
                </div>
                <div class="flex justify-between mb-4">
                    <span class="font-medium">Total:</span>
                    <span id="total" class="font-bold text-lg">R$ 0,00</span>
                </div>
                
                <div class="mb-6">
                    <h3 class="font-medium mb-2">Forma de Pagamento</h3>
                    <div class="grid grid-cols-2 gap-2">
                        <button class="payment-method bg-gray-100 py-2 px-4 rounded hover:bg-gray-200" data-method="PIX">PIX</button>
                        <button class="payment-method bg-gray-100 py-2 px-4 rounded hover:bg-gray-200" data-method="Cartão">Cartão</button>
                        <button class="payment-method bg-gray-100 py-2 px-4 rounded hover:bg-gray-200" data-method="Dinheiro">Dinheiro</button>
                        <button class="payment-method bg-gray-100 py-2 px-4 rounded hover:bg-gray-200" data-method="Boleto">Boleto</button>
                    </div>
                </div>
                
                <form id="checkoutForm" class="space-y-4">
                    <div>
                        <label for="customerName" class="block text-sm font-medium text-gray-700">Nome Completo</label>
                        <input type="text" id="customerName" required class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-green-500 focus:border-green-500">
                    </div>
                    
                    <div>
                        <label for="customerAddress" class="block text-sm font-medium text-gray-700">Endereço</label>
                        <input type="text" id="customerAddress" required class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-green-500 focus:border-green-500">
                    </div>
                    
                    <div>
                        <label for="customerPhone" class="block text-sm font-medium text-gray-700">Telefone</label>
                        <input type="tel" id="customerPhone" required class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-green-500 focus:border-green-500">
                    </div>
                    
                    <div>
                        <label for="customerCity" class="block text-sm font-medium text-gray-700">Cidade</label>
                        <input type="text" id="customerCity" required class="mt-1 block w-full border border-gray-300 rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-green-500 focus:border-green-500">
                    </div>
                    
                    <button type="submit" class="w-full bg-green-600 text-white py-3 px-4 rounded-md hover:bg-green-700 font-medium flex items-center justify-center">
                        <i class="fas fa-whatsapp mr-2"></i> Enviar Pedido por WhatsApp
                    </button>
                </form>
            </div>
        </div>
    </div>

    <!-- Overlay -->
    <div id="overlay" class="fixed inset-0 bg-black bg-opacity-50 z-40 hidden"></div>

    <script>
        // Sample product data - in a real app, this would come from a database
        const products = [
            // Abafadores/Protetores
            { id: 1, name: "ABAFADOR PROTETOR AURICULAR CONCHA", price: 24.80, category: "Proteção" },
            { id: 2, name: "ABRACADEIRA NYLON 100X2,5MM", price: 0.10, category: "Fixação" },
            { id: 3, name: "ABRACADEIRA NYLON 150X2,5MM", price: 0.10, category: "Fixação" },
            { id: 4, name: "ABRACADEIRA NYLON 150X3,5MM", price: 0.12, category: "Fixação" },
            { id: 5, name: "ABRACADEIRA NYLON 150X3,6MM", price: 0.13, category: "Fixação" },
            { id: 6, name: "ABRACADEIRA NYLON 200X2,5MM", price: 0.12, category: "Fixação" },
            { id: 7, name: "ABRACADEIRA NYLON 2500X3,6MM", price: 0.20, category: "Fixação" },
            { id: 8, name: "ABRACADEIRA NYLON 300X4,8", price: 0.40, category: "Fixação" },
            { id: 9, name: "ABRACADEIRA NYLON 400 X 4,8MM", price: 0.55, category: "Fixação" },
            
            // Madeiras
            { id: 100, name: "MADEIRA 07 X 06 AP", price: 26.16, category: "Madeiras", unit: "MT" },
            { id: 101, name: "MADEIRA 07 X 06 DE 1,50 MT", price: 39.12, category: "Madeiras" },
            { id: 102, name: "MADEIRA 07 X 06 DE 2,00 MT", price: 51.95, category: "Madeiras" },
            { id: 103, name: "MADEIRA 07 X 06 DE 3,00 MT", price: 77.89, category: "Madeiras" },
            { id: 104, name: "MADEIRA 12 X 06 AP", price: 41.18, category: "Madeiras", unit: "MT" },
            { id: 105, name: "MADEIRA 15 X 06 AP", price: 52.12, category: "Madeiras", unit: "MT" },
            { id: 106, name: "MADEIRA 20 X 06 AP", price: 69.67, category: "Madeiras", unit: "MT" },
            { id: 107, name: "MADEIRA 25 X 06 AP", price: 85.08, category: "Madeiras", unit: "MT" },
            
            // Ferragens
            { id: 200, name: "PARAFUSO FRANCES 1/2 X 10", price: 6.60, category: "Ferragens" },
            { id: 201, name: "PARAFUSO FRANCES 1/2 X 11", price: 10.50, category: "Ferragens" },
            { id: 202, name: "PARAFUSO FRANCES 1/2 X 12", price: 10.70, category: "Ferragens" },
            { id: 203, name: "PARAFUSO FRANCES 1/2 X 3.1/2", price: 3.20, category: "Ferragens" },
            { id: 204, name: "PARAFUSO FRANCES 1/2 X 4", price: 3.10, category: "Ferragens" },
            { id: 205, name: "PARAFUSO FRANCES 1/2 X 5", price: 4.90, category: "Ferragens" },
            
            // Hidráulica
            { id: 300, name: "BOIA CX DAGUA 1/2 AMANCO", price: 12.90, category: "Hidráulica" },
            { id: 301, name: "BOIA CX DAGUA 1/2 ASTRA", price: 14.44, category: "Hidráulica" },
            { id: 302, name: "BOIA CX DAGUA 1/2 VIQUA/KRONA", price: 8.80, category: "Hidráulica" },
            { id: 303, name: "BOIA CX DAGUA 3/4 AMANCO", price: 14.10, category: "Hidráulica" },
            { id: 304, name: "BOIA CX DAGUA HASTE ABS FORTLEV", price: 11.60, category: "Hidráulica" },
            
            // Elétrica
            { id: 400, name: "CABO DUPLEX 10MM MEGATRON", price: 3.59, category: "Elétrica", unit: "MT" },
            { id: 401, name: "CABO DUPLEX 16MM MEGATRON", price: 4.50, category: "Elétrica", unit: "MT" },
            { id: 402, name: "CABO TRIPLEX 10MM MEGATRON", price: 5.00, category: "Elétrica", unit: "MT" },
            { id: 403, name: "CABO TRIPLEX 16MM MEGATRON", price: 9.70, category: "Elétrica", unit: "MT" },
            
            // Tintas
            { id: 500, name: "TINTA ACR BEMALAR 18 L BRANCO GELO", price: 185.90, category: "Tintas" },
            { id: 501, name: "TINTA ACR BEMALAR 18 L BRANCO NEVE", price: 185.90, category: "Tintas" },
            { id: 502, name: "TINTA ACR BEMALAR 3600 AM OURO", price: 39.80, category: "Tintas" },
            { id: 503, name: "TINTA ACR BEMALAR 3600 AMEIXA", price: 39.80, category: "Tintas" },
            { id: 504, name: "TINTA ACR BEMALAR 3600 CAMURCA", price: 39.80, category: "Tintas" },
            
            // Ferramentas
            { id: 600, name: "MARTELO 25MM CABO MADEIRA FAMASTIL", price: 39.50, category: "Ferramentas" },
            { id: 601, name: "MARTELO 25MM CABO FIBRA TRAMONTINA", price: 33.90, category: "Ferramentas" },
            { id: 602, name: "MARTELO 27MM CABO MADEIRA FAMASTIL", price: 35.20, category: "Ferramentas" },
            { id: 603, name: "MARTELO 29MM CABO MADEIRA FAMASTIL", price: 39.20, category: "Ferramentas" },
            { id: 604, name: "MARTELO CABO FIBRA 25MM AQUATOOLS", price: 39.80, category: "Ferramentas" },
            
            // Telhas
            { id: 700, name: "TELHA AMERICANA CER. MINAS NATURAL", price: 2.85, category: "Telhas" },
            { id: 701, name: "TELHA AMERICANA RESINADA CER. MINAS", price: 3.05, category: "Telhas" },
            { id: 702, name: "TELHA AMERICANA SANTA CATARINA BRANCA RESINADA", price: 4.80, category: "Telhas" },
            { id: 703, name: "TELHA AMERICANA TEC NATURAL", price: 3.10, category: "Telhas" },
            { id: 704, name: "TELHA AMERICANA TEC RESINADA", price: 3.20, category: "Telhas" },
            
            // Pisos e Revestimentos
            { id: 800, name: "PISO 13010 ALASKA 57X57", price: 36.90, category: "Pisos", unit: "M2" },
            { id: 801, name: "PISO 170048 58X58", price: 36.90, category: "Pisos", unit: "M2" },
            { id: 802, name: "PISO 3301 DRITTO CZ 57X57", price: 38.90, category: "Pisos", unit: "M2" },
            { id: 803, name: "REVESTIMENTO 160135 32X58", price: 34.90, category: "Revestimentos", unit: "M2" },
            { id: 804, name: "REVESTIMENTO 240000 32X58", price: 34.50, category: "Revestimentos", unit: "M2" },
            
            // Portas e Janelas
            { id: 900, name: "PORTA ACOMAD 2,15 X 65 MOGNO ESQ", price: 358.50, category: "Portas" },
            { id: 901, name: "PORTA ACOMAD 2,15 X 65 MOGNO ESQ BRANCO", price: 397.80, category: "Portas" },
            { id: 902, name: "PORTA ALUM C/ POSTIGO 210 X 86 DIR", price: 675.00, category: "Portas" },
            { id: 903, name: "JANELA ALUM 02 F 1,0 X 1,0", price: 224.40, category: "Janelas" },
            { id: 904, name: "JANELA ALUM 02 F 1,0 X 1,20", price: 247.35, category: "Janelas" },
            
            // Tijolos e Blocos
            { id: 1000, name: "TIJOLO FURADO 19 X 19 X 14", price: 1.45, category: "Tijolos" },
            { id: 1001, name: "TIJOLO FURADO 29 X 19 X 09 REQUEIMADO", price: 1.45, category: "Tijolos" },
            { id: 1002, name: "TIJOLO FURADO 29X19X09 08 FUROS", price: 1.45, category: "Tijolos" },
            { id: 1003, name: "BLOCO CONCRETO 09x19x39 C/ FUNDO", price: 5.40, category: "Blocos" },
            { id: 1004, name: "BLOCO CONCRETO 09x19x39 VAZADO", price: 5.40, category: "Blocos" },
            
            // Cimento e Argamassa
            { id: 1100, name: "CIMENTO CPII AZUL MONTES CLAROS", price: 39.90, category: "Cimento", unit: "SC" },
            { id: 1101, name: "CIMENTO CSN CPII 50KG", price: 37.90, category: "Cimento", unit: "SC" },
            { id: 1102, name: "CIMENTO LIZ VERM CPII", price: 40.00, category: "Cimento", unit: "SC" },
            { id: 1103, name: "ARGAMASSA AC-I 20 KG FASSA BORTOLO", price: 15.00, category: "Argamassa" },
            { id: 1104, name: "ARGAMASSA AC-I 20KG ALPHAVILLE", price: 15.50, category: "Argamassa" },
            
            // Areia e Pedra
            { id: 1200, name: "AREIA LAVADA FINA", price: 99.90, category: "Areia", unit: "M3" },
            { id: 1201, name: "AREIA LAVADA GROSSA", price: 115.50, category: "Areia", unit: "M3" },
            { id: 1202, name: "AREIA PRETA", price: 81.10, category: "Areia", unit: "M3" },
            { id: 1203, name: "PEDRA DE MAO BRITADA", price: 243.60, category: "Pedra", unit: "M3" },
            { id: 1204, name: "BRITA 0", price: 261.50, category: "Pedra", unit: "M3" },
            { id: 1205, name: "PEDRA M3", price: 241.50, category: "Pedra", unit: "M3" },
            { id: 1206, name: "PEDRA MAO - CARRINHO", price: 28.00, category: "Pedra" },
            { id: 1207, name: "PEDRA REDONDA CX 1000LT 1,21 X 1,21 ARDOSIA", price: 132.80, category: "Pedra" },

            // Caixas d'água e Tanques
            { id: 1210, name: "CX DAGUA 10000LT C/ TP FORTLEV", price: 6192.60, category: "Hidráulica" },
            { id: 1211, name: "CX DAGUA 1000LT C/ TP FORTLEV", price: 478.50, category: "Hidráulica" },
            { id: 1212, name: "CX DAGUA 2000LT C/ TP FORTLEV", price: 1235.20, category: "Hidráulica" },
            { id: 1213, name: "CX DAGUA 3000LT C/ TP FORTLEV", price: 2131.50, category: "Hidráulica" },
            { id: 1214, name: "CX DAGUA 310LT C/ TP FORTLEV", price: 270.90, category: "Hidráulica" },
            { id: 1215, name: "CX DAGUA 500 C/TP FORTLEV", price: 295.00, category: "Hidráulica" },
            { id: 1216, name: "CX DAGUA 5000LT C/ TP POLIETILENO FORTLEV", price: 3160.50, category: "Hidráulica" },
            { id: 1217, name: "CX TANQUE 1000LT FORTLEV", price: 903.50, category: "Hidráulica" },
            { id: 1218, name: "CX TANQUE 2000LT FORTLEV", price: 1863.00, category: "Hidráulica" },
            { id: 1219, name: "CX TANQUE 3000LT FORTLEV", price: 2980.00, category: "Hidráulica" },

            // Caixas diversas
            { id: 1220, name: "CX FERRAM BAU N1 FERCAR", price: 69.50, category: "Ferramentas" },
            { id: 1221, name: "CX FERRAM BAU N2", price: 79.92, category: "Ferramentas" },
            { id: 1222, name: "CX GORDURA MALTON QUAD 29 X 53 C/ CESTO", price: 122.40, category: "Ferramentas" },
            { id: 1223, name: "CX GORDURA MALTON REDONDA 42LT C/ CESTO", price: 92.75, category: "Ferramentas" },
            { id: 1224, name: "CX INSPECAO ESG 100 TIGRE", price: 435.73, category: "Hidráulica" },
            { id: 1225, name: "CX LUZ FERRO FMD", price: 3.85, category: "Elétrica" },
            { id: 1226, name: "CX LUZ FERRO FMS", price: 2.15, category: "Elétrica" },
            { id: 1227, name: "CX LUZ PLAST 04 X 02 FORTLEV", price: 2.05, category: "Elétrica" },
            { id: 1228, name: "CX LUZ PLAST 04 X 02 PRETA PT", price: 0.73, category: "Elétrica" },
            { id: 1229, name: "CX LUZ PLAST 04 X 02 TRAMONTINA", price: 1.15, category: "Elétrica" },
            { id: 1230, name: "CX LUZ PLAST 04 X 04 FORTLEV", price: 4.90, category: "Elétrica" },
            { id: 1231, name: "CX LUZ PLAST 04 X 04 TIGRE/ AMANCO", price: 4.90, category: "Elétrica" },
            { id: 1232, name: "CX LUZ PLAST 04 X 04 TRAMONTINA", price: 2.80, category: "Elétrica" },
            { id: 1233, name: "CX LUZ PLAST 04 X 04AM BRASIP", price: 2.20, category: "Elétrica" },
            { id: 1234, name: "CX LUZ PLAST 3X3 F.M T/AK OCTOGONAL", price: 2.25, category: "Elétrica" },
            { id: 1235, name: "CX LUZ PLAST FMS", price: 2.35, category: "Elétrica" },
            { id: 1236, name: "CX LUZ PLAST P/ LAJE 30CM", price: 4.60, category: "Elétrica" },
            { id: 1237, name: "CX P/ ACOPL SAVEIRO PT", price: 188.40, category: "Hidráulica" },
            { id: 1238, name: "CX P/ MASSA 160LT FORTLEV", price: 179.80, category: "Ferramentas" },
            { id: 1239, name: "CX P/ MASSA 40LT FORTLEV", price: 43.50, category: "Ferramentas" },
            { id: 1240, name: "CX P/ MASSA AZUL 20L FORTLEV", price: 21.50, category: "Ferramentas" },
            { id: 1241, name: "CX P/ MASSA PLAST. PRETA 19-22LT", price: 12.90, category: "Ferramentas" },
            { id: 1242, name: "CX P/ NICHO MULTI 40X30 TEX TRIAN BG COZIMAX", price: 221.38, category: "Revestimentos" },
            { id: 1243, name: "CX P/ NICHO MULTI 40X30 TEX TRIAN BRANCO COZIMAX", price: 221.38, category: "Revestimentos" },
            { id: 1244, name: "CX P/ NICHO MULTI 40X30 TEX TRIAN PT COZIMAX", price: 221.38, category: "Revestimentos" },
            { id: 1245, name: "CX P/ NICHO MULTI 60X30 TEX TRIAN BG COZIMAX", price: 290.18, category: "Revestimentos" },
            { id: 1246, name: "CX P/ NCHO MULTI 60X30 TEX TRIAN BRANCO COZIMAX", price: 290.18, category: "Revestimentos" },
            { id: 1247, name: "CX P/ NICHO MULTI 60X30 TEX TRIAN PT COZIMAX", price: 290.18, category: "Revestimentos" },
            { id: 1248, name: "CX P/ PADRAO CM1 ACOVAZ", price: 104.00, category: "Hidráulica" },
            { id: 1249, name: "CX P/ PADRAO CM2 ACOVAZ", price: 192.00, category: "Hidráulica" },
            { id: 1250, name: "CX P/ACOPLAR 21160 CELITE", price: 266.43, category: "Hidráulica" },
            { id: 1251, name: "CX P/ACOPLAR C/ MECAN BRANCA SABATINI", price: 404.63, category: "Hidráulica" },
            { id: 1252, name: "CX P/ACOPLAR C/ MECAN BRANCO EL MISTI SABATINI", price: 435.12, category: "Hidráulica" },
            { id: 1253, name: "CX P/ACOPLAR C/ MECAN COLOR SABATINI SABATINI", price: 465.31, category: "Hidráulica" },
            { id: 1254, name: "CX PASSAGEM 15 X 15 TIGRE", price: 41.28, category: "Hidráulica" },
            { id: 1255, name: "CX PASSAGEM 20 X 20 TIGRE", price: 65.32, category: "Hidráulica" },
            { id: 1256, name: "CX PASSAGEM MALLTON 35X44X42 52LT", price: 117.30, category: "Hidráulica" },
            { id: 1257, name: "CX SIFON 25 QUAD150X150X50 AMANCO", price: 42.50, category: "Hidráulica" },
            { id: 1258, name: "CX SIFON 250 X 250 X 75/100 HERK", price: 77.90, category: "Hidráulica" },
            { id: 1259, name: "CX SIFON 250X172X50 KRONA", price: 71.50, category: "Hidráulica" },
            { id: 1260, name: "CX SIFON 63 QUAD100X100X50 AMANCO", price: 26.50, category: "Hidráulica" },
            
            // Ferro
            { id: 1300, name: "FERRO CA 50 1/2", price: 91.40, category: "Ferro" },
            { id: 1301, name: "FERRO CA 50 1/4", price: 23.50, category: "Ferro" },
            { id: 1302, name: "FERRO CA 50 16MM (5/8)", price: 152.20, category: "Ferro" },
            { id: 1303, name: "FERRO CA 50 20MM (3/4)", price: 239.90, category: "Ferro" },
            { id: 1304, name: "FERRO REDONDO 1", price: 276.50, category: "Ferro" },
            
            // Louças e Metais
            { id: 1400, name: "VASO +CX ACOPL S/ SIFAO APR SABATINI AREIA", price: 972.60, category: "Louças" },
            { id: 1401, name: "VASO +CX ACOPL SAVEIRO BC", price: 562.49, category: "Louças" },
            { id: 1402, name: "TORNEIRA M 2068 GIR COZINHA PAREDE FLEX C55 1/4PRETO", price: 230.00, category: "Metais" },
            { id: 1403, name: "TORNEIRA M LAV 6510 GIR MESA C 68 PERFETTO 1/4 VT", price: 392.50, category: "Metais" },
            { id: 1404, name: "CHUVEIRO ACQUA DUO ULT BLK/CR 127/5500", price: 795.90, category: "Metais" },
            
            // Iluminação
            { id: 1500, name: "LUMINARIA 1 X E-27 BCO/PTO", price: 14.40, category: "Iluminação" },
            { id: 1501, name: "LUMINARIA 2 X E-27 BCO/PTO", price: 19.90, category: "Iluminação" },
            { id: 1502, name: "LAMPADA LED 15W ELGIN", price: 6.40, category: "Iluminação" },
            { id: 1503, name: "LAMPADA LED 9 W TRAMONTINA", price: 3.90, category: "Iluminação" },
            { id: 1504, name: "SPOT LED EMB QUAD 5W", price: 7.00, category: "Iluminação" },
            
            // Segurança
            { id: 1600, name: "CADEADO 20 MM PADO", price: 15.90, category: "Segurança" },
            { id: 1601, name: "CADEADO 25 MM PAPAIZ", price: 18.90, category: "Segurança" },
            { id: 1602, name: "CADEADO 30 MM PADO", price: 21.90, category: "Segurança" },
            { id: 1603, name: "CADEADO 35 MM PAPAIZ", price: 26.00, category: "Segurança" },
            { id: 1604, name: "FECHADURA 10770 ROSETA MODENA CROMADA", price: 53.90, category: "Segurança" },
            
            // Jardim
            { id: 1700, name: "MANGUEIRA 1/2 TRANC LAR/ VERD/ AM", price: 4.20, category: "Jardim", unit: "MT" },
            { id: 1701, name: "MANGUEIRA 3/4X3,0 LISA VD", price: 6.90, category: "Jardim", unit: "MT" },
            { id: 1702, name: "REGADOR PLAST 10LT", price: 19.20, category: "Jardim" },
            { id: 1703, name: "TESOURA PODA PROF TRAMONTINA", price: 58.90, category: "Jardim" },
            { id: 1704, name: "RASTELO (ANCINHO 14 DENTES) TRAMONTINA", price: 15.20, category: "Jardim" },
            
            // Limpeza
            { id: 1800, name: "VASSOURA CERDAS NATURAIS", price: 24.90, category: "Limpeza" },
            { id: 1801, name: "PA LIXEIRA COM CABO", price: 39.90, category: "Limpeza" },
            { id: 1802, name: "RODO PROFISSIONAL", price: 29.90, category: "Limpeza" },
            { id: 1803, name: "BALDE PEDREIRO 608P ATLAS", price: 14.50, category: "Limpeza" },
            { id: 1804, name: "LUVA RASPA C/C", price: 12.90, category: "Limpeza" },
            
            // Metalon
            { id: 1900, name: "METALON 100X40 CH 14", price: 289.40, category: "Metalon" },
            { id: 1901, name: "METALON 100X40 CH 16", price: 203.50, category: "Metalon" },
            { id: 1902, name: "METALON 100X50 CH 14", price: 296.80, category: "Metalon" },
            { id: 1903, name: "METALON 15 X 15 GALV", price: 15.50, category: "Metalon" },
            { id: 1904, name: "METALON 150X50 CH 14", price: 458.20, category: "Metalon" },
            { id: 1905, name: "METALON 150X50 CH 16", price: 350.00, category: "Metalon" },
            { id: 1906, name: "METALON 20 X 20 GALV", price: 22.70, category: "Metalon" },
            { id: 1907, name: "METALON 20X20 CH 18", price: 54.00, category: "Metalon" },
            { id: 1908, name: "METALON 20X20 CH 20", price: 41.50, category: "Metalon" },
            { id: 1909, name: "METALON 20X30 CH 18", price: 64.84, category: "Metalon" },
            { id: 1910, name: "METALON 20X30 CH 20", price: 46.80, category: "Metalon" },
            { id: 1911, name: "METALON 30X30 CH 18", price: 87.60, category: "Metalon" },
            { id: 1912, name: "METALON 40X20 CH 18", price: 74.90, category: "Metalon" },
            { id: 1913, name: "METALON 40X20 CH 20", price: 57.90, category: "Metalon" },
            { id: 1914, name: "METALON 40X40 CH 18", price: 96.70, category: "Metalon" },
            { id: 1915, name: "METALON 50X30 CH 16", price: 115.00, category: "Metalon" },
            { id: 1916, name: "METALON 50X30 CH 18", price: 91.80, category: "Metalon" },
            { id: 1917, name: "METALON 50X30 CH 20", price: 71.50, category: "Metalon" },
            { id: 1918, name: "METALON 50X50 CH 14", price: 226.20, category: "Metalon" },
            { id: 1919, name: "METALON 50X50 CH 18", price: 136.50, category: "Metalon" },
            { id: 1920, name: "METALON 70X30 CH 18", price: 125.01, category: "Metalon" },
            { id: 1921, name: "METALON 80X40 CH 14", price: 253.60, category: "Metalon" },
            { id: 1922, name: "METALON 80X40 CH 16", price: 195.20, category: "Metalon" },
            { id: 1923, name: "METALON 80X40 CH 18", price: 144.30, category: "Metalon" },

            // Churrasqueira
            { id: 2000, name: "CHURRASQUEIRA - FOGAO - FORNO - KIT 3PC TRIO MARFIM 2,58CM", price: 3450.00, category: "Churrasqueiras" },
            { id: 2001, name: "CHURRASQUEIRA - FOGAO - FORNO - KIT 3PC TRIO VM/BC 2,58CM", price: 3450.00, category: "Churrasqueiras" },
            { id: 2002, name: "CHURRASQUEIRA - FOGAO - KIT 02PC", price: 2850.00, category: "Churrasqueiras" },
            { id: 2003, name: "CHURRASQUEIRA ALUMINIO PQ BAFINHO", price: 218.50, category: "Churrasqueiras" },
            { id: 2003, name: "CHURRASQUEIRA ALUMINIO REGULAVEL", price: 362.50, category: "Churrasqueiras" },
            { id: 2004, name: "CHURRASQUEIRA BAFINHO CHAPA C/ PE", price: 225.20, category: "Churrasqueiras" },
            { id: 2005, name: "CHURRASQUEIRA BOTIJAO", price: 181.50, category: "Churrasqueiras" },
            { id: 2006, name: "CHURRASQUEIRA CRAQUADA BAR 01", price: 181.00, category: "Churrasqueiras" },
            { id: 2007, name: "CHURRASQUEIRA CRAQUADA BAR 02", price: 209.50, category: "Churrasqueiras" },
            { id: 2008, name: "CHURRASQUEIRA CRAQUEADA CAMPING", price: 138.90, category: "Churrasqueiras" },
            { id: 2009, name: "CHURRASQUEIRA ELETRICO 127V/1200W FAME", price: 147.90, category: "Churrasqueiras" },
            { id: 2010, name: "CHURRASQUEIRA ESPETEIRA MEDIA", price: 240.00, category: "Churrasqueiras" },
            { id: 2011, name: "CHURRASQUEira MINI TIJOLINHO CONHAQUE", price: 675.00, category: "Churrasqueiras" },
            { id: 2012, name: "CHURRASQUEIRA MINI TIJOLINHO PT/BCO", price: 675.00, category: "Churrasqueiras" },
            { id: 2013, name: "CHURRASQUEIRA MINI TIJOLINHO VERM/CONC", price: 675.00, category: "Churrasqueiras" },
            { id: 2014, name: "CHURRASQUEIRA P03 ESPETO FRIZO CONCRETO VM", price: 855.00, category: "Churrasqueiras" },
            { id: 2015, name: "CHURRASQUEIRA P03 ESPETO MARFIM", price: 855.00, category: "Churrasqueiras" },
            { id: 2016, name: "CHURRASQUEIRA P04 ESPETO FRIZO CONCRETO VM", price: 1005.00, category: "Churrasqueiras" },
            { id: 2017, name: "CHURRASQUEIRA P04 ESPETO FRIZO VM/BR", price: 1005.00, category: "Churrasqueiras" },
            { id: 2018, name: "CHURRASQUEIRA P04 ESPETO MARFIM", price: 1005.00, category: "Churrasqueiras" },
            { id: 2019, name: "CHURRASQUEIRA P04 ESPETO PT", price: 1005.00, category: "Churrasqueiras" },
            { id: 2020, name: "CHURRASQUEIRA P05 ESPETO FRIZO BCO VM", price: 1155.00, category: "Churrasqueiras" },
            { id: 2021, name: "CHURRASQUEIRA P05 ESPETO MARF", price: 1155.00, category: "Churrasqueiras" },
            { id: 2022, name: "CHURRASQUEIRA P4 FOGAO - FORNO - KIT 3PC TRIO PREDIAL", price: 3650.00, category: "Churrasqueiras" }
            { id: 2023, name: "CHURRASQUEIRA PREDIAL P3 CONCRETO", price: 855.00, category: "Churrasqueiras" },
            { id: 2024, name: "CHURRASQUEIRA PREDIAL P4 CONCRETO", price: 1005.00, category: "Churrasqueiras" },
        ];

        // Shopping cart
        let cart = [];
        let selectedPaymentMethod = null;

        // DOM elements
        const productsGrid = document.getElementById('productsGrid');
        const cartButton = document.getElementById('cartButton');
        const cartCount = document.getElementById('cartCount');
        const cartSidebar = document.getElementById('cartSidebar');
        const closeCart = document.getElementById('closeCart');
        const cartItems = document.getElementById('cartItems');
        const emptyCartMessage = document.getElementById('emptyCartMessage');
        const subtotalElement = document.getElementById('subtotal');
        const totalElement = document.getElementById('total');
        const overlay = document.getElementById('overlay');
        const checkoutForm = document.getElementById('checkoutForm');
        const searchInput = document.getElementById('searchInput');
        const categoryButtons = document.querySelectorAll('.category-btn');

        // Initialize the app
        function init() {
            renderProducts(products);
            setupEventListeners();
        }

        // Render products to the grid
        function renderProducts(productsToRender) {
            productsGrid.innerHTML = '';
            
            if (productsToRender.length === 0) {
                productsGrid.innerHTML = '<p class="text-gray-500 col-span-full text-center py-12">Nenhum produto encontrado</p>';
                return;
            }
            
            productsToRender.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'material-card bg-white rounded-lg shadow-md overflow-hidden';
                productCard.innerHTML = `
                    <div class="p-4">
                        <h3 class="font-semibold text-lg text-gray-800 mb-1">${product.name}</h3>
                        <p class="text-green-600 font-bold mb-1">R$ ${product.price.toFixed(2).replace('.', ',')}${product.unit ? ` / ${product.unit}` : ''}</p>
                        ${['Telhas', 'Tijolos', 'Blocos'].includes(product.category) ? 
                          `<p class="text-green-800 text-sm mb-3">R$ ${(product.price * 1000).toFixed(2).replace('.', ',')} / 1000 un</p>` : 
                          ''}
                        <div class="flex flex-col space-y-2">
                            ${['Telhas', 'Tijolos', 'Blocos'].includes(product.category) ? `
                            <div class="flex items-center space-x-2">
                                <button class="quantity-option bg-gray-200 px-3 py-1 rounded hover:bg-gray-300 ${product.unit ? 'w-full' : ''}" data-id="${product.id}" data-quantity="1">
                                    Unidade: R$ ${product.price.toFixed(2).replace('.', ',')}
                                </button>
                                <button class="quantity-option bg-green-600 text-white px-3 py-1 rounded hover:bg-green-700" data-id="${product.id}" data-quantity="1000">
                                    1000 un: R$ ${(product.price * 1000).toFixed(2).replace('.', ',')}
                                </button>
                            </div>
                            ` : ''}
                            <button class="add-to-cart bg-green-600 text-white py-2 px-4 rounded hover:bg-green-700 transition w-full" data-id="${product.id}" data-quantity="1">
                                <i class="fas fa-cart-plus mr-1"></i> Adicionar
                            </button>
                        </div>
                    </div>
                `;
                productsGrid.appendChild(productCard);
            });
        }

        // Setup event listeners
        function setupEventListeners() {
            // Cart toggle
            cartButton.addEventListener('click', toggleCart);
            closeCart.addEventListener('click', toggleCart);
            overlay.addEventListener('click', toggleCart);

            // Add to cart buttons (delegated event)
            document.addEventListener('click', function(e) {
                // Quantity option selection
                if (e.target.classList.contains('quantity-option') || e.target.closest('.quantity-option')) {
                    const button = e.target.classList.contains('quantity-option') ? e.target : e.target.closest('.quantity-option');
                    const productId = parseInt(button.dataset.id);
                    const quantity = parseInt(button.dataset.quantity);
                    
                    // Update the add to cart button quantity
                    const addButton = button.closest('.flex-col').querySelector('.add-to-cart');
                    addButton.dataset.quantity = quantity;
                    
                    // Highlight selected option
                    button.closest('.flex').querySelectorAll('.quantity-option').forEach(btn => {
                        btn.classList.remove('bg-green-600', 'text-white', 'hover:bg-green-700');
                        btn.classList.add('bg-gray-200', 'hover:bg-gray-300');
                    });
                    button.classList.remove('bg-gray-200', 'hover:bg-gray-300');
                    button.classList.add('bg-green-600', 'text-white', 'hover:bg-green-700');
                }
                
                // Add to cart
                if (e.target.classList.contains('add-to-cart') || e.target.closest('.add-to-cart')) {
                    const button = e.target.classList.contains('add-to-cart') ? e.target : e.target.closest('.add-to-cart');
                    const productId = parseInt(button.dataset.id);
                    const quantity = parseInt(button.dataset.quantity);
                    addToCart(productId, quantity);
                }
                
                // Remove item from cart
                if (e.target.classList.contains('remove-item') || e.target.closest('.remove-item')) {
                    const button = e.target.classList.contains('remove-item') ? e.target : e.target.closest('.remove-item');
                    const productId = parseInt(button.dataset.id);
                    removeFromCart(productId);
                }
                
                // Increase quantity
                if (e.target.classList.contains('increase-quantity') || e.target.closest('.increase-quantity')) {
                    const button = e.target.classList.contains('increase-quantity') ? e.target : e.target.closest('.increase-quantity');
                    const productId = parseInt(button.dataset.id);
                    changeQuantity(productId, 1);
                }
                
                // Decrease quantity
                if (e.target.classList.contains('decrease-quantity') || e.target.closest('.decrease-quantity')) {
                    const button = e.target.classList.contains('decrease-quantity') ? e.target : e.target.closest('.decrease-quantity');
                    const productId = parseInt(button.dataset.id);
                    changeQuantity(productId, -1);
                }
                
                // Payment method selection
                if (e.target.classList.contains('payment-method') || e.target.closest('.payment-method')) {
                    const button = e.target.classList.contains('payment-method') ? e.target : e.target.closest('.payment-method');
                    selectPaymentMethod(button.dataset.method);
                }
            });

            // Search functionality
            searchInput.addEventListener('input', function() {
                const searchTerm = this.value.toLowerCase();
                
                if (searchTerm.length > 0) {
                    const filteredProducts = products.filter(product => 
                        product.name.toLowerCase().includes(searchTerm)
                    );
                    renderProducts(filteredProducts);
                    
                    // Highlight search terms in product names
                    document.querySelectorAll('.material-card h3').forEach(title => {
                        const text = title.textContent;
                        const regex = new RegExp(searchTerm, 'gi');
                        const newText = text.replace(regex, match => 
                            `<span class="search-highlight">${match}</span>`
                        );
                        title.innerHTML = newText;
                    });
                } else {
                    renderProducts(products);
                }
            });

            // Category filtering
            categoryButtons.forEach(button => {
                button.addEventListener('click', function() {
                    const category = this.textContent.trim();
                    
                    // Update active button
                    categoryButtons.forEach(btn => {
                        btn.classList.remove('bg-green-600', 'text-white');
                        btn.classList.add('bg-gray-100', 'text-gray-800', 'hover:bg-gray-200');
                    });
                    
                    if (category === 'Todos') {
                        renderProducts(products);
                        this.classList.remove('bg-gray-100', 'text-gray-800', 'hover:bg-gray-200');
                        this.classList.add('bg-green-600', 'text-white');
                    } else {
                        const filteredProducts = products.filter(product => 
                            product.category === category
                        );
                        renderProducts(filteredProducts);
                        this.classList.remove('bg-gray-100', 'text-gray-800', 'hover:bg-gray-200');
                        this.classList.add('bg-green-600', 'text-white');
                    }
                });
            });

            // Checkout form submission
            checkoutForm.addEventListener('submit', function(e) {
                e.preventDefault();
                
                if (cart.length === 0) {
                    alert('Seu carrinho está vazio!');
                    return;
                }
                
                if (!selectedPaymentMethod) {
                    alert('Selecione uma forma de pagamento!');
                    return;
                }
                
                const name = document.getElementById('customerName').value;
                const address = document.getElementById('customerAddress').value;
                const phone = document.getElementById('customerPhone').value;
                const city = document.getElementById('customerCity').value;
                
                // Format the WhatsApp message
                let message = `Eu sou ${name}, rua ${address}, cidade ${city}, telefone ${phone}. Meu pedido é:\n\n`;
                
                cart.forEach(item => {
                    message += `${item.quantity}x ${item.name} - R$ ${(item.price * item.quantity).toFixed(2).replace('.', ',')}\n`;
                });
                
                message += `\nTotal: R$ ${calculateTotal().toFixed(2).replace('.', ',')}\n`;
                message += `Forma de pagamento: ${selectedPaymentMethod}`;
                
                // Encode the message for URL
                const encodedMessage = encodeURIComponent(message);
                
                // WhatsApp API link
                const whatsappLink = `https://wa.me/5538999902267?text=${encodedMessage}`;
                
                // Open WhatsApp in a new tab
                window.open(whatsappLink, '_blank');
                
                // Reset form and cart
                checkoutForm.reset();
                cart = [];
                updateCart();
                toggleCart();
                selectedPaymentMethod = null;
                updatePaymentMethodButtons();
            });
        }

        // Toggle cart visibility
        function toggleCart() {
            cartSidebar.classList.toggle('translate-x-full');
            overlay.classList.toggle('hidden');
            document.body.classList.toggle('overflow-hidden');
        }

        // Add product to cart
        function addToCart(productId, quantity = 1) {
            const product = products.find(p => p.id === productId);
            
            if (product) {
                const existingItem = cart.find(item => item.id === productId);
                
                if (existingItem) {
                    existingItem.quantity += quantity;
                } else {
                    cart.push({
                        id: product.id,
                        name: product.name,
                        price: product.price,
                        quantity: quantity
                    });
                }
                
                updateCart();
                
                // Show feedback
                const feedback = document.createElement('div');
                feedback.className = 'fixed bottom-4 right-4 bg-green-500 text-white px-4 py-2 rounded shadow-lg animate-bounce';
                feedback.innerHTML = `<i class="fas fa-check-circle mr-2"></i> ${product.name} adicionado ao carrinho!`;
                document.body.appendChild(feedback);
                
                setTimeout(() => {
                    feedback.remove();
                }, 2000);
            }
        }

        // Remove product from cart
        function removeFromCart(productId) {
            const itemIndex = cart.findIndex(item => item.id === productId);
            
            if (itemIndex !== -1) {
                cart.splice(itemIndex, 1);
                updateCart();
            }
        }
        
        // Change product quantity
        function changeQuantity(productId, change) {
            const item = cart.find(item => item.id === productId);
            
            if (item) {
                item.quantity += change;
                
                // Remove if quantity reaches 0
                if (item.quantity <= 0) {
                    removeFromCart(productId);
                } else {
                    updateCart();
                }
            }
        }

        // Update cart UI
        function updateCart() {
            // Update cart count
            const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
            cartCount.textContent = totalItems;
            
            // Update cart items list
            cartItems.innerHTML = '';
            
            if (cart.length === 0) {
                emptyCartMessage.classList.remove('hidden');
                subtotalElement.textContent = 'R$ 0,00';
                totalElement.textContent = 'R$ 0,00';
                return;
            }
            
            emptyCartMessage.classList.add('hidden');
            
            cart.forEach(item => {
                const itemElement = document.createElement('div');
                itemElement.className = 'cart-item flex justify-between items-center py-3 border-b border-gray-200';
                itemElement.innerHTML = `
                    <div class="flex-1">
                        <h4 class="font-medium text-gray-800">${item.name}</h4>
                        <p class="text-sm text-gray-600">R$ ${item.price.toFixed(2).replace('.', ',')} x ${item.quantity}</p>
                    </div>
                    <div class="flex items-center">
                        <div class="flex items-center mr-4">
                            <button class="decrease-quantity bg-gray-200 px-2 py-1 rounded-l hover:bg-gray-300" data-id="${item.id}">
                                <i class="fas fa-minus text-xs"></i>
                            </button>
                            <span class="quantity-display bg-gray-100 px-3 py-1 text-center w-10">${item.quantity}</span>
                            <button class="increase-quantity bg-gray-200 px-2 py-1 rounded-r hover:bg-gray-300" data-id="${item.id}">
                                <i class="fas fa-plus text-xs"></i>
                            </button>
                        </div>
                        <span class="font-medium mr-4">R$ ${(item.price * item.quantity).toFixed(2).replace('.', ',')}</span>
                        <button class="remove-item text-red-500 hover:text-red-700" data-id="${item.id}">
                            <i class="fas fa-trash"></i>
                        </button>
                    </div>
                `;
                cartItems.appendChild(itemElement);
            });
            
            // Update totals
            const subtotal = calculateSubtotal();
            const total = calculateTotal();
            
            subtotalElement.textContent = `R$ ${subtotal.toFixed(2).replace('.', ',')}`;
            totalElement.textContent = `R$ ${total.toFixed(2).replace('.', ',')}`;
        }

        // Calculate subtotal
        function calculateSubtotal() {
            return cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
        }

        // Calculate total (could include taxes, shipping, etc.)
        function calculateTotal() {
            return calculateSubtotal();
        }

        // Select payment method
        function selectPaymentMethod(method) {
            selectedPaymentMethod = method;
            updatePaymentMethodButtons();
        }

        // Update payment method buttons UI
        function updatePaymentMethodButtons() {
            document.querySelectorAll('.payment-method').forEach(button => {
                if (button.dataset.method === selectedPaymentMethod) {
                    button.classList.remove('bg-gray-100', 'hover:bg-gray-200');
                    button.classList.add('bg-green-600', 'text-white', 'hover:bg-green-700');
                } else {
                    button.classList.remove('bg-green-600', 'text-white', 'hover:bg-green-700');
                    button.classList.add('bg-gray-100', 'hover:bg-gray-200');
                }
            });
        }

        // Initialize the app
        init();
    </script>
</body>
</html>
