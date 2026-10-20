# Escenarios que elegi y porque:

Elegi escenarios de solapamiento parcial en test/crear_reserva_test.dart linea 56 y 71, tambien de reservas contenidas y que contienen otras reservas en test/crear_reserva_test.dart linea 86 y 101 y por ultimo un caso de intervalos identicos en el mismo .dart linea 158, estos escenarios comprueban que se rechacen todos estos conflictos.
Tambien inclui casos para reservas consecutivas en ambos ordenes en el mismo .dart lineas 116 y 130 y reservas en salas diferentes en linea 144 para que no se rechacen solicitudes en el mismo horario si es en otra sala

# Riesgo mas grave del repositorio

El riesgo mas grave es que esta expuesta una clave service_role en lib/data/supabase_config.dart. Como la app usa esta clave para inicializar supabase y el readme indica que se usa, si fuera a ser valida eso puede permitir que cualquiera acceda a la base de dates, eludiendo las politicas de seguridad y es un riesgo para todos los datos que se guarden en supabase

# La regla protege la app real?

No al 100%, CrearReserva consulta las reservas que ya existen y comprueba el solapamiento antes de guardar, esto se ve en lib/domain/crear_reserva.dart linea 16 y 18. Pero aunque en el main.dart porporciona el caso de uso a la pantalla en las lineas 14 y 26, el metodo _reservar inserta todo directamente al supabase, esto se ve en lib/presentation/reserva_page.dart linea 58 y 60, evitando la validacion.
Aparte la migracion SQL solo comprueba que el fin sea despues del inicio en el migracion.sql linea 11, no hay restriccion contra solapamiento, tambien hay un problema de que de que la consulta y el guardado son operaciones diferentes una esta en crear_reserva.dart linea 16 y otro en la linea 28.
Para proteger al 100% la aplicacion se necesita que se use el CrearReserva desde el ui y aplicar la restriccion del solapamiento en supabase.