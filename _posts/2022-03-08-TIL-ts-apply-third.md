---
title: "π 3/8 TS -  μ μ§μ μΌλ‘ μ μ©νκΈ° (3)"
date: 2022-03-08 9:32:00 +0900
categories: [TIL]
tags: [typescript]
---

- μΌλ¨ anyλ‘ μ€μ μ ν΄λ ν, μ‘°κΈ λ μ μ ν νμμΌλ‘ λ°κΏλκ°κΈ°
- string, any λ±λ κ°λ₯νμ§λ§ νμμ κ°μ΄ νμ λ κ²½μ°, μ§μ  νμ μ μΈνλ κ²λ μ’λ€

  ```jsx
  enum CovidStatus {
  	Confirmed = 'confirmed',
  	Deaths = 'deaths',
  	Recovered = 'recovered'
  }

  const fetchCovidCountry(id: string, status: CovidStatus): string {
     //...
  }
  ```

- new Date(), getTime() λ±κ³Ό κ°μ λ΄μ₯ js λΌμ΄λΈλ¬λ¦¬ κ°μ κ²½μ°λ μλμΌλ‘ νμμ΄ μΆλ‘ λλ€.
