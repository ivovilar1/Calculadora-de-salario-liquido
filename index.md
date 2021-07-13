<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora Salário líquido</title>
    <link rel="stylesheet" href="style/style.css">
    <script>
        
        
        function mostrar(){
            document.getElementById('resultado-visivel').style.visibility = 'visible';
            calcular();            
        }
        
            

        function calcularInss(){
            var salario = parseInt(document.getElementById("salario-bruto").value);
            var inss = document.getElementById("inss");
            var descontoinss = document.getElementById("desconto-inss");
            
            if(salario <=1100){
                var salarioComDesconto = salario * 0.075;
                var SalarioComParcelaADeduzir = salario - salarioComDesconto;
                inss.innerHTML = "7.5%";
                descontoinss.innerHTML = "R$ " + salarioComDesconto.toFixed(2);
                return [SalarioComParcelaADeduzir, salarioComDesconto] ;
            }

            else if(salario >= 1100.01 && salario <2203.48){
                var salarioComDesconto = salario * 0.09;
                var SalarioComParcelaADeduzir = salarioComDesconto - 16.50;
                var salarioComOsDescontos = salario - SalarioComParcelaADeduzir ;
                inss.innerHTML = "9%";
                descontoinss.innerHTML = "R$ " + SalarioComParcelaADeduzir.toFixed(2);
                return [salarioComOsDescontos,SalarioComParcelaADeduzir] ; 
            }else if(salario >=2203.49 && salario < 3305.22){
                var salarioComDesconto = salario * 0.12;
                var SalarioComParcelaADeduzir = salarioComDesconto - 82.60;
                var salarioComOsDescontos = salario - SalarioComParcelaADeduzir ;
                inss.innerHTML = "12%";
                descontoinss.innerHTML = "R$ " + SalarioComParcelaADeduzir.toFixed(2);
                return [salarioComOsDescontos,SalarioComParcelaADeduzir] ; 
            }else if(salario >=3305.23 && salario < 6433.57){
                var salarioComDesconto = salario * 0.14;
                var SalarioComParcelaADeduzir = salarioComDesconto - 148.70;
                var salarioComOsDescontos = salario - SalarioComParcelaADeduzir ;
                inss.innerHTML = "14%";
                descontoinss.innerHTML = "R$ " + SalarioComParcelaADeduzir.toFixed(2);
                return [salarioComOsDescontos,SalarioComParcelaADeduzir] ; 
            }else{
                var SalarioComParcelaADeduzir = salario - 751.99;
                var salarioComOsDescontos = salario - SalarioComParcelaADeduzir ;
                var parcelaTeto = 751.99;
                inss.innerHTML = "Teto";
                descontoinss.innerHTML = "R$ " + parcelaTeto.toFixed(2);
                return [SalarioComParcelaADeduzir, parcelaTeto] ; 
            }
        }

        

        function calcularIrrf(){
            var irrf = document.getElementById("irrf");
            var descontoirrf = document.getElementById("desconto-irrf");
            var numeroDependentes = parseInt(document.getElementById("numeroDependentes").value);
            var pensao = parseInt(document.getElementById("pensao").value);

            var baseDeCalculo = pensao + (numeroDependentes * 189.59);
            var salarioListaInss = calcularInss();
            
           
            var salarioComDescontoID = salarioListaInss[0] - baseDeCalculo;
            
                if( salarioComDescontoID <= 1903.98){
                    irrf.innerHTML = "0%";
                    descontoirrf.innerHTML = "R$ 0";
                    valorDoDescontoIrrf = 0;
                    return [valorDoDescontoIrrf, valorDoDescontoIrrf];
            
                 }else if(salarioComDescontoID > 1903.99 && salarioComDescontoID <= 2826.65){
                    var descontoIrrf = salarioComDescontoID * 0.075;
                    var valorDoDescontoIrrf = descontoIrrf - 142.8 ;
                    var valorDoDescontoIrrf1 = descontoIrrf - 142.8 ;
                    var salarioComIrrf = salarioComDescontoID - valorDoDescontoIrrf; 
                    irrf.innerHTML = "7,5%";
                    descontoirrf.innerHTML = "R$ " + valorDoDescontoIrrf1.toFixed(2); // toFixed retorna uma String
                    return [valorDoDescontoIrrf,valorDoDescontoIrrf];
                }else if(salarioComDescontoID >2826.66 && salarioComDescontoID <= 3751.05){
                    var descontoIrrf = salarioComDescontoID * 0.15;
                    var valorDoDescontoIrrf = descontoIrrf - 354.80 ;
                    var valorDoDescontoIrrf1 = descontoIrrf - 354.80
                    var salarioComIrrf = salarioComDescontoID - valorDoDescontoIrrf;
                    descontoirrf.innerHTML = "R$ " + valorDoDescontoIrrf1.toFixed(2);
                    irrf.innerHTML = "15%";
                    return [valorDoDescontoIrrf,valorDoDescontoIrrf];
                }else if(salarioComDescontoID >3751.06 && salarioComDescontoID <= 4664.68){
                    var descontoIrrf = salarioComDescontoID * 0.225;
                    var valorDoDescontoIrrf = descontoIrrf - 636.13;
                    var valorDoDescontoIrrf1 = descontoIrrf - 636.13;
                    var salarioComIrrf = salarioComDescontoID - valorDoDescontoIrrf;
                    descontoirrf.innerHTML = "R$ " + valorDoDescontoIrrf1.toFixed(2);
                    irrf.innerHTML = "22,5%";
                    return [valorDoDescontoIrrf,valorDoDescontoIrrf];
                    
                }else {
                    var descontoIrrf = salarioComDescontoID * 0.275;
                    var valorDoDescontoIrrf = descontoIrrf - 869.36;
                    var valorDoDescontoIrrf1 = descontoIrrf - 869.36;
                    var salarioComIrrf = salarioComDescontoID - valorDoDescontoIrrf;
                    descontoirrf.innerHTML = "R$ " + valorDoDescontoIrrf1.toFixed(2);
                    irrf.innerHTML = "27,5%";
                    return [valorDoDescontoIrrf,valorDoDescontoIrrf];
                    
            }
        }  

        

        function calcular(){
            var salario = parseInt(document.getElementById("salario-bruto").value);
            if(salario >0){
            
            var planoDeSaude = parseInt(document.getElementById("planoDeSaude").value);
            var pat = parseInt(document.getElementById("pat").value);
            var pensao = parseInt(document.getElementById("pensao").value);
            var outrosDescontos = parseInt(document.getElementById("outrosDescontos").value);
            var salariofinal = document.getElementById("salario-provento");
           
            salariofinal.innerHTML = "R$ " + salario;
            
            

            var salarioresultado = document.getElementById("salarioresultado");
            
            
            var salariototal = document.getElementById("salariototal");
            salariototal.innerHTML = "R$ " + salario;
           
            
           var descontototal = document.getElementById("descontototal");
            var descontostotais = document.getElementById("descontostotais");
    
            var descontoDoInss = calcularInss();
            var descontoDoIrrf = calcularIrrf();

            var somaDosDescontosExtras = pat + planoDeSaude + outrosDescontos + pensao;
            descontostotais.innerHTML = "R$ " + somaDosDescontosExtras;


            var SomaDoDescontoIsIrEx = descontoDoInss[1] + descontoDoIrrf[1] + somaDosDescontosExtras;
            
            
            
            descontototal.innerHTML = "R$ " + SomaDoDescontoIsIrEx.toFixed(2);
            var salarioResultado = salario - SomaDoDescontoIsIrEx;
            salarioresultado.innerHTML = "R$ " + salarioResultado.toFixed(2);
            }
        else{
            alert('Salário tem que ser maior que 0')
        }
                            

        }
 
    </script>
    
</head>
<body>
    <div id="todos-campos">
        <p>Calculadora</p>
        <div class="form-group">
            <label class="salario-provento">Salário Bruto:</label>
                <div class='input-campo'>
                    <span class="cifrao">R$</span>
                    <input  class="campo" type="text" id="salario-bruto" placeholder="0" value="0" />
                </div>
        
            <label class="lblcampo">Número de dependentes:</label>
                <div class='input-campo'>
                    <input class="campo2" type="text" id="numeroDependentes" placeholder="0" value="0"/>
                </div>
        
            <label class="lblcampo">Pensão Alimentícia:</label>
                <div class='input-campo'>
                    <span class="cifrao">R$</span>
                    <input  class="campo" type="text" id="pensao" placeholder="0" value="0" />
                </div>
        
            <label class="lblcampo">PAT (Programa de Alimentação do trabalhador):</label>
                <div class='input-campo'>
                    <span class="cifrao">R$</span>
                    <input  class="campo" type="text" id="pat" placeholder="0" value="0" />
                </div>
        
            <label class="lblcampo">Plano de Saúde:</label>
                <div class='input-campo'>
                    <span class="cifrao">R$</span>
                    <input class="campo" type="text" id="planoDeSaude" placeholder="0" value="0" />
                </div>
        
            <label class="lblcampo">Outros Descontos:</label>
                <div class='input-campo'>
                    <span class="cifrao">R$</span>
                    <input class="campo" type="text" id="outrosDescontos" placeholder="0" value="0" />
                </div>
        
                <button class="btn-calcular" title="Clique aqui para calcular" onclick='mostrar()' >Calcular</button>
                <button class="btn-novo" title="Clique aqui para novo" onclick="document.location.reload(true)">Novo</button>
               
        </div>                  
        </div>
    </div>
    <div id=resultado-visivel>
        <table class="campos1">
            <thead>
                <th class="campo-descricao">Descrição</th>
                <th class="campo-aliquota">Alíquota</th>
                <th class="campo-proventos">Proventos</th>
                <th class="campo-descontos-cabecalho">Descontos</th>
            </thead>
            <tbody>
                <tr >
                    <td class="campo-salario">Salário Bruto</td>
                    <td></td>
                    <td id="salario-provento"></td>
                    <td></td>
                </tr>
                <tr>
                    <td class="campo-inss">INSS</td>
                    <td id="inss"></td>
                    <td></td>
                    <td id="desconto-inss"></td>
                </tr>
                <tr>
                    <td class="campo-irrf">IRRF</td>
                    <td id="irrf"></td>
                    <td></td>
                    <td id="desconto-irrf"></td>
                </tr>
                <tr>
                    <td class="campo-descontos">Outros Descontos</td>
                    <td></td>
                    <td></td>
                    <td id="descontostotais"></td>
                </tr>
                <tr>
                    <td class="campo-total">Total</td>
                    <td></td>
                    <td id="salariototal"></td>
                    <td id="descontototal"></td>
                </tr>
                <tr>
                    <td class="campo-resultado">Resultado</td>
                    <td></td>
                    <td></td>
                    <td id="salarioresultado"></td>
                </tr>
            </tbody>
        </table>
    </div>
    
</body>
</html>
