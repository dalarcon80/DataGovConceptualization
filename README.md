# AgenticGov — Agente de Contexto y Proceso (esqueleto)

Este repositorio contiene un scaffold para implementar el "Agente de Contexto y Proceso" usando .NET y servicios de GCP (Vertex AI, Vector Search, Storage, Pub/Sub, Firestore).

Proyectos:
- AgenticGov.Knowledge (Class Library): lógica RAG (extracción, chunking, embeddings, indexación y búsqueda).
- AgenticGov.Agents.Context (Worker Service): consumidor de tareas (Pub/Sub), orquesta RAG y genera cuestionarios a SMEs.
- AgenticGov.WebApp.SME (ASP.NET Core Web API): UI/API simple para que SMEs respondan cuestionarios.

Requisitos:
- .NET 8+ SDK
- Cuenta GCP con permisos para: Vertex AI, Vertex Vector Search, Cloud Storage, Firestore, Pub/Sub.
- Service Account JSON con las credenciales y variable de entorno GOOGLE_APPLICATION_CREDENTIALS apuntando al fichero.

Primera configuración:
1. Clonar repo y abrir con Visual Studio / dotnet CLI.
2. Ajustar appsettings.json en cada proyecto (nombres de bucket, topics, collections).
3. Implementar parsers específicos (PDF, Office, OCR para diagramas).
4. Conectar llamadas reales a Vertex AI Embeddings / Gemini y Vertex Vector Search (puntos marcados como TODO).
5. Publicar/ejecutar:
   - Deploy del Worker en Cloud Run / GKE / Compute Engine como servicio que lea Pub/Sub.
   - Deploy de WebApp como Cloud Run (o App Engine), configurando autenticación del SME.
6. Crear pipeline de ingest periódica (Cloud Scheduler -> Pub/Sub -> Worker).

Siguientes pasos recomendados:
- Implementar extracción robusta para PDF y diagramas (OCR).
- Completar integración con Vertex AI Embeddings y Vector Search.
- Añadir pruebas unitarias y e2e.
- Añadir autenticación para SMEs (IAP, OAuth, SSO).
- Mejorar UI para cuestionarios y versióning del conocimiento.
