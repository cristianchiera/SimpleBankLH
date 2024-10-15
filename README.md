
# SimpleBank LH

## Descripción

`SimpleBank` es un contrato inteligente de Ethereum desarrollado en Solidity para gestionar un sistema bancario básico. Los usuarios pueden registrarse, realizar depósitos y retiros de ETH, y el contrato incluye una función de tesorería que acumula comisiones por cada retiro. Este proyecto incluye pruebas unitarias y scripts de interacción.

## Funcionalidades del Contrato

1. **Registro de Usuarios**: Permite que nuevos usuarios se registren proporcionando su nombre y apellido. Cada usuario registrado tiene un balance inicial de 0.
2. **Depósito de ETH**: Permite a los usuarios registrados depositar ETH en su cuenta dentro del contrato.
3. **Retiro de ETH**: Los usuarios registrados pueden retirar ETH. Cada retiro incurre en una comisión, que se almacena en la tesorería del contrato.
4. **Balance de Tesorería**: Acumula las comisiones de las transacciones de retiro y permite al propietario retirar fondos de la tesorería.

## Variables Principales

- `owner`: Dirección del propietario del contrato, quien tiene privilegios adicionales.
- `treasury`: Dirección donde se acumulan las comisiones.
- `fee`: Comisión aplicada en cada retiro (en puntos básicos).
- `treasuryBalance`: Balance acumulado en la tesorería.

## Funciones Principales

- **register(string firstName, string lastName)**: Registra un nuevo usuario.
- **deposit()**: Permite a los usuarios registrados depositar ETH en su cuenta.
- **withdraw(uint256 amount)**: Permite a los usuarios registrados retirar ETH con una comisión deducida.
- **getTreasuryBalance()**: Retorna el balance acumulado en la tesorería.

## Pruebas Incluidas

Las pruebas para el contrato `SimpleBank` están implementadas en `test/SimpleBankTest.ts` y cubren lo siguiente:

1. **Deployment**: Verifica que la dirección del propietario y la tesorería se configuren correctamente.
2. **Registro de Usuarios**:
   - Prueba que un usuario pueda registrarse.
   - Verifica que no se permita un doble registro para el mismo usuario.
3. **Depósitos**:
   - Asegura que los usuarios registrados puedan depositar ETH.
   - Verifica que los usuarios no registrados no puedan realizar depósitos.
4. **Retiros**:
   - Prueba que los usuarios puedan retirar ETH y que el fee se acumule en la tesorería.
   - Verifica que los usuarios no puedan retirar más de su balance.
   - Asegura que los usuarios no registrados no puedan realizar retiros.
5. **Tesorería**:
   - Verifica que el propietario pueda retirar el balance de la tesorería.
   - Asegura que solo el propietario tenga permisos para retirar de la tesorería.
   - Verifica la función `getTreasuryBalance()` para que el balance acumulado sea el correcto.

## Scripts de Interacción

En el archivo `interactSimpleBank.ts`, se proporcionan los scripts para interactuar con el contrato en una red Ethereum. Incluye las siguientes acciones:

1. **Registro de Usuario**: Verifica si un usuario está registrado; si no, lo registra.
2. **Depósito de ETH**: Realiza un depósito en el contrato desde la cuenta del usuario.
3. **Verificación de Balance**: Consulta el balance actual del usuario en el contrato.
4. **Retiro de ETH**: Permite al usuario retirar una cantidad específica de ETH.
5. **Consulta de Propietario y Tesorería**: Verifica la dirección del propietario y la tesorería del contrato.
6. **Balance de Tesorería**: Muestra el balance acumulado en la tesorería.

## Ejecución de los Scripts

Para ejecutar los scripts de interacción:

```bash
npx hardhat help
npx hardhat test
REPORT_GAS=true npx hardhat test
npx hardhat node
npx hardhat ignition deploy ./ignition/modules/Lock.ts

```
