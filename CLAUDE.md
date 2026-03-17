# MultiSharp — CLAUDE.md

## Contexte du projet

MultiSharp est une extension Visual Studio (VSIX) pour VS 2022 qui analyse, corrige et refactore du code C#, à la manière de ReSharper.

**Contrainte fondamentale :** Zéro dépendance NuGet ajoutée aux projets analysés. Toute la logique s'exécute dans le process Visual Studio via l'extension VSIX.

## Architecture

- **Type de projet :** VSIX (`.vsixmanifest`)
- **Framework :** .NET (VSIX target pour VS 2022)
- **Analyse de code :** Roslyn embarqué dans l'extension (`Microsoft.CodeAnalysis.CSharp`)
- **Intégration VS :** MEF + VS SDK 17.x
- **Tests :** xUnit + `Microsoft.CodeAnalysis.Testing`

## Suivi de l'avancement

Voir `ROADMAP.md` pour le backlog complet avec user stories et le dashboard de statut.

## Conventions de développement

- Chaque `DiagnosticAnalyzer` dans son propre fichier sous `src/Analyzers/`
- Chaque `CodeFixProvider` dans `src/CodeFixes/` avec le même nom que son analyser
- Chaque `CodeRefactoringProvider` dans `src/Refactorings/`
- Tests unitaires obligatoires pour chaque analyser/fix via `Microsoft.CodeAnalysis.CSharp.Testing`
- Pas d'`IVsTextManager` direct quand une API Roslyn suffit

## Phases de développement

| Phase | Contenu |
|-------|---------|
| P0 | Fondations VSIX + Roslyn workspace |
| P1 | Analyseurs + Quick Fixes |
| P2 | Refactorings |
| P3 | Génération de code |
| P4 | Navigation & Recherche |
| P5 | Formatage & Style |
| P6 | Fonctionnalités avancées |
