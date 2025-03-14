
**npm** é o gerenciador de pacotes node, ele irá instalar na sua máquina um pacote para que você possa utiliza-lo em outros projetos sem precisar baixar novamente.

já o **npx** ele irá usar o pacote sem precisar baixar em sua máquina, sendo assim você irá instalar um pacote no seu projeto ou até mesmo usar esse pacote, sem baixar os arquivos em sua **máEquina**.

**Para que o npx é util?**

- Já instalou algum pacote global e precisou usá-lo pouquíssimas vezes?
- Já teve problemas de incompatibilidade com pacotes globais por diferença de versões em múltiplos projetos?
- Já sentiu que sua máquina está poluída por diversos pacotes globais?****

Quando você instala react-native em sua máquina e começa um projeto usando ele ao invés de NPX, você está usando a versão do react-native do pacote instalado em seu node_modules, já quando usa npx você usa um pacote na nuvem do node, então isso te da liberdade para usar até outras versões que não tem em sua máquina.