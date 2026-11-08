# Problemas de los que "todo el mundo se queja" que se pueden atacar con código

Fecha: 8 de noviembre de 2026
Objetivo: encontrar quejas recurrentes (Reddit, Hacker News, foros, encuestas, blogs, YouTube) que se puedan resolver con una automatización o un producto pequeño, y decidir por cuál empezar.

## 0. Veredicto en tres líneas

1. **No existe un problema "universal" sin resolver.** Todo lo que se queja todo el mundo (facturas que no pagan, WhatsApp saturado, suscripciones olvidadas, citas imposibles, correo desbordado) ya tiene entre 5 y 50 productos encima. Si la idea es "hacer la app que todos necesitan", es mala idea y hay que decirlo claro.
2. **Lo que sí hay son huecos por segmento y por precio.** Las herramientas existentes están hechas para empresas medianas de EE. UU. o Reino Unido, cobran 50 a 260 USD al mes, y dejan fuera al restaurante, al freelancer o al contador pequeño de Latinoamérica.
3. **Recomendación:** empezar por la **conciliación de liquidaciones de apps de delivery para restaurantes independientes** (Rappi, PedidosYa, Uber Eats, DiDi Food). Es un problema que toca dinero directamente, se puede resolver con un parser y un motor de cruce, y la competencia está en el segmento enterprise. Segunda opción: recordatorios de cobro por WhatsApp para quienes cobran por transferencia. Detalle en la sección 4.

## 1. Cómo se hizo y qué limitaciones tiene

- Se hicieron unas 40 búsquedas web en inglés y español sobre quejas, encuestas, hilos de foros y reseñas de software (Capterra, G2, Trustpilot, App Store).
- **Limitación importante:** la red de esta sesión bloquea el acceso directo a news.ycombinator.com, reddit.com, old.reddit.com y a las bases de datos de pain points (BigIdeasDB, IdeaFast, LaunchSaaS, MicroGaps). Se intentó crear un entorno con esos hosts permitidos y el servicio lo rechazó. Por eso los hilos de Reddit y Hacker News se leyeron a través de fragmentos del buscador y de resúmenes de terceros, no del hilo completo.
- Casi todas las cifras que circulan vienen de proveedores de software con interés en vender la solución. Se marca cada una como "proveedor" o "fuente primaria" cuando se puede distinguir. Tómalas como orden de magnitud, no como dato exacto.
- YouTube: el buscador no devuelve conteos de vistas ni rankings de videos; solo aparecen tutoriales de n8n, Make, Zapier y Claude Code. No hay señal de YouTube que no esté ya cubierta por las otras fuentes.

## 2. Mapa de quejas encontradas

Escala de "señal": cuántas fuentes independientes repiten la queja y si hay frases del tipo "pagaría por esto" o "pierdo X horas". Escala de "competencia": cuántos productos ya atacan exactamente esa queja.

| # | Queja | Quién la sufre | Evidencia (resumida) | Señal | Competencia | Viable empezar con código |
|---|---|---|---|---|---|---|
| 1 | Perseguir facturas impagas | Freelancers, oficios (plomeros, electricistas), pymes | 85 % de freelancers cobran tarde alguna vez (Remote, citado por proveedores). 29 % de facturas freelance se pagan tarde (Bonsai). 51 % de pymes LATAM con problemas de cobro (Bitness, 2026). Hilos recurrentes en r/smallbusiness, r/freelance, r/Bookkeeping según MicroGaps. | Muy alta | Muy alta: QuickBooks, Xero, FreshBooks y Zoho ya lo traen; Chaser desde 259 USD/mes; PayFlowAI 19,99 USD; en LATAM Aurora Inbox, Debitia, Wati, Kharyo, Zoye | Sí, pero solo en un nicho (ver 4.2) |
| 2 | Conciliar pagos de apps de delivery con las ventas reales | Restaurantes independientes | Comisiones hasta 30 %; cada plataforma liquida con formato distinto (DoorDash resta comisión, Uber Eats paga neto con créditos aparte, Grubhub manda PDF que no cruza con el POS). Reembolsos y ajustes que nadie reclama. Fuentes: Restaurant Business, Rosnet, OrderOut, Delaget, IQ BackOffice. | Alta | Media: existen Delaget, Rosnet, Trintech, Virturant, pero apuntan a cadenas y a EE. UU. No se encontró nada para Rappi, PedidosYa o DiDi Food orientado a locales de 1 a 3 sucursales | **Sí, el mejor candidato** |
| 3 | Contadores persiguiendo a clientes cada mes por facturas y transacciones sin clasificar | Contadores y bookkeepers con muchos clientes pequeños | LaunchSaaS cita hilos de r/Bookkeeping: "las últimas dos semanas de cada mes se van en perseguir clientes". Uncat cobra 9 USD por cliente y los reviews dicen que es caro para despachos chicos. | Alta | Media: Uncat, Client Hub, Keeper, Karbon, TaxDome (todos EE. UU., integrados con QuickBooks/Xero). En LATAM la variante es pedir CFDI/comprobantes, y no se encontró herramienta dedicada | Sí (tercera opción) |
| 4 | Responder lo mismo todo el día por WhatsApp (stock, precios, ubicación, horarios) | Microempresas LATAM | 44 % de pymes mexicanas pierden 5 a 10 horas semanales en tareas repetitivas (Alegra, Pulso Pymes 2026). 74 % de pymes LATAM con baja automatización. Desde el 1 de octubre de 2026 Meta cobra las respuestas de servicio por API después de 1 000 mensajes gratis al mes (Infobae, Simla, Molécula Digital). | Alta | Muy alta: decenas de chatbots (Wati, Aunoa, Leadsales, Asisteclick...). El cambio de precios de Meta encarece a todos | Solo como complemento de 1 o 2, no como producto principal |
| 5 | Sobreventa por stock desincronizado entre Mercado Libre y tienda propia | Vendedores ecommerce LATAM | Cancelaciones penalizan la reputación por semanas; Mercado Envíos Full complica el cruce (Profitar, Acumatica, reseñas de Bitmeli). | Media | Alta: Profitar, Bitmeli, Ventiapp, Acumatica, Mente Digital | No, el hueco ya está ocupado |
| 6 | Horas perdidas en administración general | Dueños de pymes | 11 horas semanales en administración y finanzas, el doble que en crecer el negocio (American Express UK, 1 000 encuestados, 2026, fuente primaria). 96 minutos diarios en tareas improductivas (Slack vía Forbes). | Muy alta | No aplica: es demasiado genérico para un producto | No como tal; sirve para justificar 1, 2 y 3 |
| 7 | Buscar información interna dispersa (Slack, docs, código) | Desarrolladores y equipos | Fricción número uno en el informe de Atlassian 2025 y 2026, por encima de deuda técnica; mitad de los devs pierde unas 10 horas semanales (3 500 encuestados). | Alta | Muy alta: Glean, Notion AI, Slack AI, Confluence, Copilot. Mercado enterprise | No para empezar solo |
| 8 | Flaky tests y esperas de CI | Equipos de desarrollo | 77 % dice que las pruebas inestables les quitan tiempo (LambdaTest, 1 600 QA). Google reporta 16 % de sus 4,2 millones de tests con algo de inestabilidad. | Alta | Alta: BuildPulse, Trunk, Datadog CI Visibility, Cypress Cloud, Mergify, TestDino | Técnicamente sí, comercialmente difícil |
| 9 | Código de IA "casi correcto" y revisar en vez de escribir | Desarrolladores | 66 % de 49 000 encuestados (Stack Overflow 2025, fuente primaria). 85 % dice que el cuello de botella pasó a ser revisar (GitLab 2026). | Muy alta | Muy alta y con gigantes dentro | No |
| 10 | Postular a cientos de empleos y que te ignoren | Candidatos | 53 % sufrió ghosting en el último año (Criteria vía Fortune, marzo 2026). 242 postulaciones promedio por vacante (proveedor). Hilos en Blind. | Muy alta | Alta y riesgosa: los auto-apply (LazyApply) generan baneos de LinkedIn y listas negras de reclutadores | No: el lado candidato empeora el problema para todos |
| 11 | Citas imposibles de conseguir (extranjería en España, trámites) | Inmigrantes, ciudadanos | Bots acaparan citas y las revenden desde 50 EUR; Policía desarticuló un grupo en 2024 (Friberd Legal, Cohen y Aguirre). | Muy alta | Existen servicios de alerta en zona gris (Citaping, Citalince) | **No: cualquier bot sobre el portal oficial es ilegal o lo empeora** |
| 12 | Suscripciones olvidadas | Consumidores | 28 % de consumidores de EE. UU. dice que gestionar dispositivos y suscripciones es abrumador (Deloitte vía roundup). | Media | Saturada: docenas de apps en App Store, Rocket Money, Chargeback | No |
| 13 | Apelar rechazos de seguros médicos | Pacientes y clínicas en EE. UU. | Menos del 1 % apela aunque 64 a 80 % de apelaciones se revierten (Counterforce, proveedor). | Alta | Alta y con opciones gratuitas: Claimable, Counterforce, Fight Health Insurance, Waystar | No desde LATAM |
| 14 | Documentación clínica y papeleo docente | Enfermería, docentes | 79 % de enfermeras pierde tiempo en registros improductivos (KLAS, 80 000 encuestadas, primaria). Docentes de educación especial suman 15 a 20 horas no pagadas por semana (Minnesota). | Muy alta | Alta y regulada: ambient scribes de grandes empresas | No para empezar |
| 15 | Entrada manual de facturas y recibos PDF a planilla | Bookkeepers, pymes | 3 a 5 minutos por factura; 20 a 30 horas al mes para quien procesa cientos (proveedores). | Alta | Muy alta: OCR y extracción están commoditizados | Solo como pieza de 2 o 3 |

## 3. Patrones que se repiten en todas las fuentes

- **El dolor que paga toca dinero, tiempo o riesgo.** Las listas de ideas validadas coinciden en eso y los casos 1, 2 y 3 lo cumplen; los casos de productividad personal (12, correo) no.
- **La queja número uno de quien construye productos no es construir, es conseguir usuarios.** IdeaFast (600 posts de r/indiehackers) y su informe de 26 comunidades ponen "crecimiento y conversión" como el dolor principal en 6 de 26 comunidades. Esto manda: elegir un problema donde puedas hablar en persona con 20 clientes potenciales vale más que elegir el problema más grande.
- **Las herramientas "para todos" ganan por integraciones, no por ingenio.** Zapier tiene más de 9 000 integraciones y aun así su queja número uno es el precio. Competir ahí desde cero no tiene sentido.
- **Latinoamérica está sub-servida en los tres candidatos.** Las herramientas de cobranza, conciliación y portal de contador están construidas sobre QuickBooks, Xero, DoorDash y Grubhub. Rappi, PedidosYa, DiDi Food, Mercado Pago y los CFDI del SAT casi no aparecen.
- **El cambio de precios de WhatsApp (1 de octubre de 2026) es una oportunidad y un riesgo.** Cualquier producto que mande mensajes por API tiene que diseñarse para gastar poco: usar los 1 000 mensajes gratis, agrupar avisos, y usar plantillas de utilidad, no de marketing.

## 4. Qué construir primero y por qué

### 4.1 Opción recomendada: conciliador de liquidaciones de delivery para restaurantes independientes

**Problema concreto.** El dueño recibe cada semana liquidaciones de Rappi, PedidosYa, Uber Eats y DiDi Food en formatos distintos (CSV, PDF, portal), y las ventas en su caja o POS. Nadie cruza pedido por pedido, así que comisiones mal aplicadas, reembolsos descontados dos veces, pedidos cancelados cobrados y promociones no reembolsadas se pierden. Los proveedores de EE. UU. hablan de recuperar cientos a miles de dólares al mes por local; en LATAM no hay cifra pública, que es justamente lo que hay que medir con 5 restaurantes reales.

**Por qué este y no otro.**
- Toca dinero directo: el producto se vende con "te recuperé X pesos este mes", no con "te ahorré tiempo".
- Es un problema de datos, no de integraciones con terceros: se empieza con archivos exportados del portal de cada plataforma. No hace falta API ni permiso de nadie.
- La competencia existente (Delaget, Rosnet, Trintech, IQ BackOffice) vende a cadenas y no cubre las plataformas latinoamericanas.
- Se valida rápido: pedirle a 5 restaurantes sus exportes de un mes y devolverles un reporte. Si no aparece dinero perdido, se descarta la idea en dos semanas.

**MVP mínimo (2 a 3 semanas de trabajo).**
1. Parsers para los exportes de 2 plataformas (empezar con las 2 más usadas en tu ciudad).
2. Importador de ventas desde el POS más común en la zona o desde una planilla.
3. Motor de cruce por número de pedido, hora y monto, con tolerancias.
4. Reporte de diferencias clasificado: comisión fuera de contrato, reembolso no compensado, pedido cancelado cobrado, promoción no reembolsada, pago faltante.
5. Lista de reclamos listos para pegar en el portal de la plataforma.

**Riesgos reales.** Los formatos de exporte cambian sin aviso. Algunos locales no tienen POS y venden con libreta. Las plataformas pueden tener ventanas de disputa cortas (DoorDash habla de 30 días; hay que verificar las de cada plataforma local). Si los montos recuperados son chicos, el precio tiene que ser chico y el negocio no escala solo con restaurantes de barrio.

### 4.2 Segunda opción: recordatorios de cobro para quien factura por transferencia y cobra por WhatsApp

**Hueco.** QuickBooks, Xero y compañía ya mandan recordatorios, pero solo si facturas desde ellos. El freelancer o el oficio que manda una factura por PDF y cobra por transferencia o Mercado Pago no tiene nada por debajo de 20 USD que le persiga el cobro por WhatsApp y correo. MicroGaps afirma que no hay opción standalone bajo 49 USD para quien usa Stripe o PayPal (afirmación de proveedor, sin verificar).

**Por qué es segunda y no primera.** La demanda es la más fuerte de toda la investigación, pero el mercado es el más lleno, y el diferencial ("barato y por WhatsApp") lo puede copiar cualquiera en un mes. Solo funciona si eliges un oficio concreto (por ejemplo, electricistas o diseñadores freelance de un país) y vas a buscarlos uno por uno.

### 4.3 Tercera opción: portal "me falta esto" entre contador y cliente

**Hueco.** Uncat y Client Hub resuelven esto para despachos de EE. UU. sobre QuickBooks. En LATAM el contador persigue CFDI, comprobantes y estados de cuenta por WhatsApp cada cierre. Un portal simple donde el contador marca qué falta y el cliente sube desde el celular, con recordatorios automáticos, no apareció en ninguna búsqueda en español.

**Por qué es tercera.** El cliente que paga es el contador, que tiene poco margen y muchos clientes chicos; el precio por cliente tiene que ser muy bajo. Pero la venta es fácil de probar: un solo despacho con 30 clientes ya es un piloto.

## 5. Ideas descartadas y por qué (para no volver a ellas)

- **Bots de citas (extranjería, pasaporte, SAT):** ilegal o en zona gris, y empeora el problema para los demás. Fuera.
- **Auto-apply de empleos:** genera baneos y lista negra; el problema del ghosting lo causa justamente el exceso de postulaciones automatizadas.
- **Rastreadores de suscripciones:** saturado y con baja disposición a pagar.
- **Sincronización de stock Mercado Libre y tienda propia:** hay al menos 5 proveedores activos en español.
- **Buscador de conocimiento interno, flaky tests, revisión de código con IA:** mercados enterprise o con gigantes dentro; viables como proyecto técnico, no como primer producto.
- **Documentación clínica y docente, apelaciones de seguros:** regulados y con jugadores fuertes o gratuitos.
- **Herramienta genérica "para automatizar lo que te canse":** eso ya es n8n, Make y Zapier.

## 6. Siguiente paso propuesto

1. Elegir una ciudad y listar 10 restaurantes independientes que usen al menos 2 apps de delivery.
2. Pedir a 5 de ellos el exporte de un mes de cada plataforma y su reporte de ventas.
3. Construir el parser y el cruce para esas 2 plataformas y entregarles el reporte de diferencias en una semana.
4. Si en al menos 3 de 5 aparece dinero recuperable que justifique 20 a 50 USD al mes, seguir. Si no, pasar a la opción 4.2 con el mismo método.

## 7. Fuentes consultadas

Fuentes primarias o de prensa:
- Hacker News, "Ask HN: What do you still do manually in 2026 that should be automated?": https://news.ycombinator.com/item?id=48045237
- Hacker News, "Ask HN: What developer tool do you wish existed in 2026?": https://news.ycombinator.com/item?id=46345827
- American Express UK, encuesta sobre carga administrativa (vía Asian Trader): https://www.asiantrader.biz/small-business-owners-admin-burden
- Wolters Kluwer, encuesta a dueños de negocios nuevos: https://www.wolterskluwer.com/en/expert-insights/small-business-owners-startup-concerns
- Forbes Business Council, costo oculto de las tareas administrativas: https://www.forbes.com/councils/forbesbusinesscouncil/2026/09/25/the-hidden-cost-of-administrative-tasks/
- Stack Overflow Developer Survey 2025 y 2026: https://stackoverflow.blog/2025/12/29/developers-remain-willing-but-reluctant-to-use-ai-the-2025-developer-survey-results-are-here/ y https://stackoverflow.blog/2026/10/06/the-results-of-the-2026-developer-survey-are-here/
- Atlassian, State of Developer Experience 2025 y 2026: https://www.atlassian.com/blog/bitbucket/developer-experience-report-2025 y https://www.atlassian.com/blog/development/developer-experience-report-2026
- Fortune, ghosting a candidatos en máximo de tres años: https://www.fortune.com/2026/03/20/job-seekers-arent-imagining-things-candidates-ghosted-by-employers-hit-three-year-high
- Infobae, WhatsApp Business cobrará por responder mensajes: https://www.infobae.com/tecno/2026/09/06/whatsapp-business-cobrara-por-responder-mensajes-en-2026-a-quienes-afecta-y-a-quienes-no/
- Restaurant Business, el delivery de terceros daña la economía del restaurante: https://www.restaurantbusinessonline.com/financing/third-party-delivery-hurting-restaurant-economics
- Ecosistema Startup, estudio Alegra Pulso Pymes LATAM 2026: https://ecosistemastartup.com/pymes-mexicanas-pierden-10-horas-semanales-estudio-alegra-2026-revela-barrera-de-automatizacion/
- Bitness, 51 % de pymes LATAM con problemas de cobro: https://www.bitness.pe/2026/08/pymes-latam-enfrenta-problemas-cobro.html
- Friberd Legal, citas falsas en Extranjería: https://friberdlegal.com/citas-falsas-extranjeria-mafias-bots-reventa/
- Blind, "I'm an engineer, what do you want automated": https://www.teamblind.com/post/im-an-engineer-what-do-you-want-automated-laqgwuwg
- Blind, quejas sobre ATS: https://www.teamblind.com/post/applicant-tracking-systems-rsxqdyyx
- PYMNTS, apelaciones de seguros con IA: https://www.pymnts.com/artificial-intelligence-2/2026/insurance-denials-meet-their-match-in-ai-powered-appeals/

Fuentes de proveedores y agregadores (sesgo comercial):
- MicroGaps, cobranza para freelancers: https://www.microgaps.com/gaps/invoice-collection-freelancers-ar-automation
- LaunchSaaS, ideas micro SaaS con evidencia de Reddit: https://launchsaas.org/blog/micro-saas-ideas-validated-reddit-2026
- BigIdeasDB, pain points 2026: https://bigideasdb.com/business-pain-points-2026 y https://bigideasdb.com/small-business-software-pain-points-2026
- IdeaFast, estado de los pain points en Reddit 2026: https://www.ideafast.pro/blog/state-of-reddit-pain-points-2026 y https://www.ideafast.pro/pains/indiehackers
- Substack, "This Reddit thread is a blueprint for a $100K business": https://mihais7.substack.com/p/this-reddit-thread-is-a-blueprint
- Freelancer Dashboard, herramientas de cobranza: https://freelancerdashboard.com/blog/best-freelance-invoice-software/
- Chaser, planes y precios: https://help.chaserhq.com/plans-and-pricing
- Uncat en Capterra: https://www.capterra.com/p/247759/Uncat/
- Rosnet, conciliación de delivery: https://www.rosnet.com/blog/struggling-with-delivery-service-reconciliation-this-tech-can-help
- OrderOut, qué significa conciliar liquidaciones: https://www.orderout.co/blog/reconcile-the-difference/
- Delaget, guía de delivery: https://www.delaget.com/wp-content/uploads/formidable/2/Delaget_DeliveryWellnessGuide_09.2023_v10-1.pdf
- Profitar, sobreventa Mercado Libre y Shopify: https://profitar.app/integracion/blog/evitar-sobreventa-mercado-libre-shopify
- Simla, nueva tarificación WhatsApp API: https://www.simla.com/blog/nueva-tarificacion-whatsapp-business-api
- Molécula Digital, respuestas de servicio dejan de ser gratis: https://molecula.digital/blog/whatsapp-precios-octubre-2026/
- Tecnochat, adopción de la API de WhatsApp en microempresas LATAM: https://tecnochat.com/blog/whatsapp/salto-de-adopcion-de-la-api-de-whatsapp-en-microempresas-latam
- Aurora Inbox, cobranza por WhatsApp para pymes: https://www.aurorainbox.com/2025/06/21/cobranza-por-whatsaap/
- Getpanto, estadísticas de flaky tests: https://www.getpanto.ai/blog/flaky-test-statistics
- Mergify, herramientas contra flaky tests: https://articles.mergify.com/how-to-get-rid-of-flaky-tests-lethal-tools/
- Conduit Health, documentación en enfermería: https://www.conduithealth.io/blog/should-nurses-spend-up-to-40-percent-of-their-time-on-documentation
- Readless, estadísticas de fatiga de suscripciones: https://www.readless.app/blog/subscription-fatigue-statistics-2026
- Vellum, asistentes de IA para pymes según Reddit: https://www.vellum.ai/blog/best-ai-assistant-for-small-business-reddit
- AIApplyd, herramientas de búsqueda de empleo según Reddit: https://aiapplyd.com/blog/job-search-tools-reddit-recommends-2026
- Parseur, comparación n8n, Zapier, Make: https://parseur.com/blog/zapier-n8n-make
- Tryorbye, reseña de Zapier con quejas de G2 y Trustpilot: https://www.tryorbye.com/products/zapier

## 8. Segundo filtro: escalable y fácil de vender (añadido tras revisión)

Las dos condiciones tiran en direcciones opuestas. Lo más fácil de vender en persona (restaurante, plata perdida en la mano) es lo menos escalable; lo más escalable (software autoservicio) es lo más difícil de vender sin canal. Para un desarrollador solo, "fácil de vender" tiene que significar:

1. El cliente ve el valor en dinero antes de pagar (el primer reporte lo convence, no un vendedor).
2. Alta autoservicio: conectar cuenta o subir archivo, menos de 15 minutos, sin integración a medida.
3. Un solo formato de datos para todos los clientes (una API o un exporte estándar), no un parser por cliente.
4. Los clientes ya están reunidos en algún lugar (grupos, foros, comunidades) donde un caso de éxito se propaga solo.

Puntuación de 1 a 5 de los candidatos contra esas cuatro condiciones:

| Candidato | Valor visible antes de pagar | Autoservicio | Un solo formato | Clientes reunidos | Total |
|---|---|---|---|---|---|
| Auditoría de liquidaciones para vendedores de Mercado Libre | 5 | 5 (API oficial) | 5 (una plataforma, 18 países) | 5 (grupos enormes de vendedores) | 20 |
| Recuperación de pagos fallidos (dunning) para suscripciones LATAM | 5 | 3 (depende del procesador) | 2 (Mercado Pago, dLocal, Rebill, bancos) | 3 | 13 |
| Portal contador-cliente | 2 | 4 | 4 | 4 (colegios, grupos de contadores) | 14 |
| Recordatorios de cobro por WhatsApp | 3 | 4 | 4 | 2 (freelancers dispersos) | 13 |
| Conciliación de delivery para restaurantes | 5 | 2 (exportes manuales, dueños poco técnicos) | 2 (un parser por plataforma y país) | 3 | 12 |

### 8.1 Recomendación ajustada: auditoría de liquidaciones de Mercado Libre

**Qué es.** El vendedor conecta su cuenta (API oficial de Mercado Libre). La herramienta cruza cada venta con la tabla de comisiones vigente, los cargos de envío, los reembolsos, las bonificaciones y las retenciones impositivas, y le muestra: cuánto le descontaron en total, qué cargos no cuadran con las reglas publicadas, y el texto del reclamo listo para enviar.

**Evidencia de dolor.**
- La provincia de Buenos Aires registró 2 396 denuncias contra Mercado Libre solo en los primeros cuatro meses de 2026, la empresa con más reclamos de la provincia (Conclusión, La Política Online).
- Caso citado en prensa: venta de 110 000 pesos de la que el vendedor recibió 64 577, un 42 % en comisiones y cargos (Diario Jornada).
- Quejas recurrentes en sitios de reclamos sobre "exceso de bonificaciones", "cargo no reconocido" y "retenciones de impuestos indebidas"; vendedores que dicen no entender la diferencia entre comisiones concretadas, bonificadas y CEB (TuQuejaSuma).
- Petición en Change.org pidiendo intervención de Profeco por abusos hacia vendedores en México.
- No se encontró ninguna herramienta dedicada a auditar liquidaciones. Lo que existe son calculadoras de rentabilidad (Algoritmo Digital) y analítica de ventas (Nubimetrics, Real Trends), que demuestran que los vendedores ya pagan por software.

**Por qué cumple "escalable".** Una sola API, un solo modelo de datos, 18 países con el mismo producto, cero integración a medida, soporte casi nulo una vez conectada la cuenta. El costo marginal por cliente es prácticamente cero.

**Por qué cumple "fácil de vender".** El primer reporte es la venta: "conectá tu cuenta gratis y te decimos cuánto te cobraron de más". Los vendedores están concentrados en grupos de Facebook, Telegram y foros con decenas de miles de miembros, donde un solo caso de "recuperé X pesos" se replica solo. Modelo de precio natural: gratis el diagnóstico, suscripción mensual o comisión sobre lo recuperado.

**Riesgo honesto, y es grande.** Puede que Mercado Libre cobre caro pero cobre bien. Si las quejas son "la comisión es alta" y no "la comisión está mal calculada", la herramienta no encuentra nada y el producto se reduce a "explicador de liquidaciones", que vale mucho menos. Esto se resuelve en una semana: pedir a 5 vendedores su exporte de ventas y cobros de un mes y cruzarlo a mano contra las tablas vigentes. Si no aparecen errores en al menos 2 de 5, se descarta.

Otros riesgos: dependencia total de una plataforma que puede cambiar la API o sus términos; Mercado Libre puede ver la herramienta como hostil; las tablas de comisiones cambian con frecuencia (la de Argentina cambió el 1 de septiembre de 2026) y hay que mantenerlas por país.

**MVP (2 a 3 semanas).**
1. Login con cuenta de Mercado Libre vía OAuth y lectura de órdenes, pagos, envíos y facturas de cargos.
2. Tabla de comisiones y costos de envío de un solo país, versionada por fecha de vigencia.
3. Motor que recalcula lo que debería haberse cobrado por cada venta y lo compara con lo cobrado.
4. Reporte: total descontado por categoría, lista de diferencias ordenadas por monto, texto de reclamo.
5. Empezar con Argentina o México según dónde consigas los 5 vendedores piloto.

### 8.2 Por qué las otras quedan detrás

- **Conciliación de delivery:** sigue siendo la más fácil de vender uno a uno, pero no escala sin fuerza de ventas: dueños poco técnicos, exportes manuales, un parser por plataforma y país. Buen negocio de servicios, mal producto escalable.
- **Dunning LATAM:** la recuperación de pagos fallidos tiene ROI inmediato, pero exige integrarse con cada procesador (Mercado Pago, dLocal, bancos) y ya hay jugadores regionales (Rebill, DRUO con Smart Retries en Colombia). Recurly estima 129 000 millones de dólares perdidos globalmente en 2025 por fallos de pago, así que el mercado existe, pero no es terreno para empezar solo.
- **Portal contador-cliente:** escala por canal (un contador trae 30 clientes), pero el valor no se ve antes de pagar y los contadores compran lento.
- **Recordatorios de cobro:** mercado saturado y clientes dispersos; cuesta más conseguir cada cliente de lo que paga.
