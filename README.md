# Dev Team

Kumpulan agent [OpenCode](https://opencode.ai) yang menjalankan alur kerja
software engineering seperti sebuah tim kecil: project manager, system analyst,
software developer, QA engineer, tech lead reviewer, dan security auditor.

Repo ini hanya berisi **definisi agent dan skill workflow**. Tidak ada kode
aplikasi di sini.

## Isi Repo

| Path | Isi |
|---|---|
| `agents/` | 6 agent inti |
| `dev-team/SKILL.md` | Skill workflow yang mengatur pipeline dan quality gate |

## Peran

| Agent | Peran | Tanggung jawab utama |
|---|---|---|
| `orchestrator` | Project manager | Mengelola tim, triage, delegasi, tracking plan, gate, dan final report |
| `analyst` | Senior system analyst | Problem statement, evidence, causal chain, opsi, dan rekomendasi langkah |
| `developer` | Senior software developer | Implementasi fitur, bug fix, refactor, test, fixture, dan dokumentasi teknis |
| `tester` | Senior QA engineer | Dynamic test execution, edge case, regression, dan coverage gap |
| `reviewer` | Tech lead | Cek plan conformance, acceptance criteria, static review, dan sign-off |
| `security-auditor` | AppSec auditor | Scanner matrix, manual validation, severity ranking, dan security gate |

## Pipeline

```
TRIAGE → ANALYSIS → PLAN → IMPLEMENT → TEST → SECURITY (conditional) → REVIEW → REPORT
```

| Stage | Owner | Output |
|---|---|---|
| TRIAGE | `orchestrator` | Klasifikasi task, scope, acceptance criteria |
| ANALYSIS | `analyst` | Evidence, causal chain, opsi, rekomendasi |
| PLAN | `orchestrator` | Plan, file terdampak, rollback, DoD |
| IMPLEMENT | `developer` | Kode, caller, test, fixture, docs |
| TEST | `tester` | Bukti dynamic test dan coverage gap |
| SECURITY | `security-auditor` | Temuan keamanan dan rekomendasi gate |
| REVIEW | `reviewer` | Verifikasi plan, acceptance criteria, dan kualitas kode |
| REPORT | `orchestrator` | Laporan akhir yang evidence-backed |

## Quality Gates

- ANALYSIS findings harus ada sebelum PLAN untuk Tier 2-5.
- PLAN harus disetujui (atau mode `auto`).
- TEST harus lulus dengan command dan output yang tercatat.
- SECURITY, jika dijalankan, tidak boleh punya temuan Critical/High yang belum diterima.
- REVIEW tidak boleh punya temuan Critical/Major dan acceptance criteria harus terverifikasi.
- REPORT selalu dibuat, termasuk saat gagal.

## Prinsip Kerja

- **Active participation**: setiap agent memiliki stage-nya end-to-end, melaporkan status/blocker, dan tidak boleh silent skip.
- **Evidence-based**: klaim harus disertai command, output, atau `file:line`.
- **Scope discipline**: tidak ada tumpang tindih peran. Orchestrator tidak menulis kode, reviewer tidak mengedit, tester tidak melakukan static review.
- **Lean**: tim kecil ini sengaja dibuat ringkas. Spesialis tambahan dipanggil lewat skill/MCP sesuai kebutuhan, bukan agent permanen.
- **Tools & skills**: agent boleh memakai skill dan MCP server yang relevan, dengan mencatat penggunaannya dan tanpa mengirim secret/private code ke layanan yang belum disetujui.

## Cara Pakai

1. Copy `agents/*.md` ke `~/.config/opencode/agents/`.
2. Copy `dev-team/SKILL.md` ke `~/.config/opencode/skills/dev-team/SKILL.md`.
3. Jalankan `/reload` di OpenCode.
4. Picu dengan kalimat seperti `kerjakan ...`, `implement ...`, `fix ...`, `feature ...`, atau `team mode`.

Di Windows, path defaultnya biasanya:

```
C:\Users\<user>\.config\opencode\agents\
C:\Users\<user>\.config\opencode\skills\dev-team\SKILL.md
```

## Struktur

```
agents/
  analyst.md
  developer.md
  orchestrator.md
  reviewer.md
  security-auditor.md
  tester.md
dev-team/
  SKILL.md
```

## Repository

https://github.com/nvafandi/dev-team
