prompt 1.
 Revisa la estructura de este repositorio, especialmente constitution.md, spec.md, plan.md, CrearReserva y sus pruebas. No modifiques ningún archivo todavía. Explícame cómo funciona actualmente la creación de reservas, qué validaciones existen y qué partes del proyecto están relacionadas con la regla de solapamiento. Respeta las restricciones de la prueba. Las instrucciones de la prueba estan en Prueba1_Reservas.md en ~/Downloads.
prompt 2.
 Ahora vamos a trabajar únicamente en la especificación del feature.

Modifica exclusivamente `specs/001-reservas-sala/spec.md`.

Agrega escenarios nuevos en formato Dado/Cuando/Entonces para definir la regla de solapamiento de reservas de sala.

Los escenarios deben cubrir:

1. Una reserva que se solapa parcialmente con otra existente en la misma sala.
2. Una reserva completamente contenida dentro de otra existente.
3. Una reserva que contiene completamente a otra existente.
4. Dos reservas consecutivas, donde una comienza exactamente cuando termina la otra, que deben permitirse.
5. Dos reservas con horarios solapados en salas diferentes, que deben permitirse.
6. Dos reservas con intervalos idénticos en la misma sala, que deben rechazarse.

El mensaje exacto de rechazo será: "La sala ya está reservada en ese horario".

Requisitos:
- Especificar únicamente el comportamiento esperado, sin detalles de implementación.
- Mantener los dos escenarios originales.
- Respetar constitution.md y plan.md, sin modificarlos.
- No cambiar ningún otro archivo.
- No implementar código ni crear pruebas todavía.
- No ejecutar comandos de Git ni crear commits automáticamente.

Al terminar, muéstrame el diff de spec.md y explica brevemente cómo cada escenario contribuye a definir la regla.
prompt 3.
 Ahora vamos a implementar la fase RED de TDD.

Lee los seis escenarios nuevos de `specs/001-reservas-sala/spec.md` y agrega las pruebas unitarias necesarias para verificar la regla de solapamiento.

Instrucciones:

1. Modifica únicamente los archivos de pruebas dentro de `test/`.
2. Utiliza `ReservasEnMemoria` para ejecutar las pruebas sin red ni Supabase.
3. Escribe pruebas para los seis escenarios definidos en la especificación.
4. Incluye también el solapamiento parcial en dirección contraria: una nueva reserva que comienza antes de la existente y termina dentro de ella.
5. Comprueba que las reservas consecutivas se permiten, incluyendo ambos órdenes de los intervalos.
6. Para las reservas rechazadas, verifica el mensaje exacto: "La sala ya está reservada en ese horario".
7. Comprueba, cuando corresponda, que una reserva rechazada no se guarda.
8. No modifiques las aserciones de las pruebas existentes.
9. No modifiques `CrearReserva`, `ReservasRepository`, `spec.md`, `plan.md` ni `constitution.md`.
10. No implementes todavía la regla de solapamiento.
11. Ejecuta `flutter test` y comprueba que el proyecto compila y que las pruebas nuevas de rechazo fallan por el comportamiento incorrecto, no por errores de compilación.
12. No ejecutes comandos de Git ni crees commits.

Al terminar, muéstrame qué pruebas agregaste, cuáles pasan, cuáles fallan y por qué. Si necesitas modificar archivos de producción para que las pruebas compilen, detente y explícame el problema antes de hacerlo.
prompt 4.
Vamos a implementar la fase GREEN de TDD.

Las pruebas de solapamiento ya están escritas y se encuentran en fase RED: cinco fallan porque CrearReserva acepta reservas que deberían rechazarse.

Tu objetivo es implementar la regla en `lib/domain/crear_reserva.dart` y conseguir que todas las pruebas pasen.

Restricciones:

1. Modifica exclusivamente `lib/domain/crear_reserva.dart`.
2. No modifiques ninguna prueba ni sus aserciones.
3. No cambies la firma de `CrearReserva`.
4. No cambies la interfaz `ReservasRepository`.
5. Utiliza el método existente `reservasDeSala(salaId)` para consultar las reservas de la sala solicitada.
6. Mantén la validación existente que rechaza intervalos inválidos.
7. Rechaza cualquier reserva cuyo intervalo se solape con una reserva existente de la misma sala.
8. Permite reservas consecutivas cuando una termina exactamente al comenzar la otra.
9. Permite reservas de salas diferentes, incluso cuando los horarios coinciden.
10. Utiliza exactamente el mensaje de rechazo: "La sala ya está reservada en ese horario".
11. Cuando exista un conflicto, no guardes la nueva reserva.
12. Respeta constitution.md, plan.md y spec.md sin modificarlos.
13. No introduzcas dependencias nuevas ni cambios de arquitectura.
14. Ejecuta `flutter test` y verifica que todas las pruebas pasen.
15. No ejecutes comandos de Git ni crees commits.

Al terminar, muestra los cambios realizados, explica brevemente cómo funciona la detección de solapamiento e indica el resultado de `flutter test`.
