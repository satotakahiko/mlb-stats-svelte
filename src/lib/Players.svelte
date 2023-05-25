<script lang="ts">
  import Player from "./Player.svelte"

  console.log("import.meta.env", [
    import.meta.env.VITE_MICROCMS_SERVICE_DOMAIN,
    import.meta.env.VITE_MICROCMS_API_KEY
])
  
  type Stat = {
    name: string
    personId: number
    group: "pitching" | "hitting"
    team: string
    league: "American League" | "National League"
    stat: Array<any> | null
  }[]

  type Api = {
    name: string
    url: string
    stat?: Array<any> | null
  }[]

  const api: Api = [
    {
      name: "大谷 翔平（投手）",
      url: "https://statsapi.mlb.com/api/v1/people/660271/stats?stats=season&group=pitching"
    },
    {
      name: "大谷 翔平（打者）",
      url: "https://statsapi.mlb.com/api/v1/people/660271/stats?stats=season&group=hitting"
    },
    {
      name: "ダルビッシュ・セファット・ファリード・有",
      url: "https://statsapi.mlb.com/api/v1/people/506433/stats?stats=season&group=pitching"
    },
    {
      name: "前田 健太",
      url: "https://statsapi.mlb.com/api/v1/people/628317/stats?stats=season&group=pitching"
    },
    {
      name: "千賀 滉大",
      url: "https://statsapi.mlb.com/api/v1/people/673540/stats?stats=season&group=pitching"
    },
    {
      name: "菊池 雄星",
      url: "https://statsapi.mlb.com/api/v1/people/579328/stats?stats=season&group=pitching"
    },
    {
      name: "藤浪 晋太郎",
      url: "https://statsapi.mlb.com/api/v1/people/660261/stats?stats=season&group=pitching"
    },
    {
      name: "吉田 正尚",
      url: "https://statsapi.mlb.com/api/v1/people/807799/stats?stats=season&group=hitting"
    },
    {
      name: "鈴木 誠也",
      url: "https://statsapi.mlb.com/api/v1/people/673548/stats?stats=season&group=hitting"
    },
    {
      name: "筒香嘉智",
      url: "https://statsapi.mlb.com/api/v1/people/660294/stats?stats=season&group=hitting"
    },
  ]

  type Stats = {
    name: string
    team: string | null
    league: string | null
    stat: Array<any> | null
  }[]

  const stats = [] as Stats

  api.forEach((items, i) => {
    fetch(items.url)
    .then((response) => response.json())
    .then((data) => {
      const hasStats = !!data.stats.length

      if(hasStats) {
        stats.push({
          name: api[i].name,
          team: data.stats[0].splits[0].team.name,
          league: data.stats[0].splits[0].league.name,
          stat: data.stats[0].splits[0].stat
        })
      } else {
        stats.push({
          name: api[i].name,
          team: null,
          league: null,
          stat: null
        })
      }
    })
  })
  console.log("stats", {stats})
</script>

<div class="players">
  <!-- {#each players as player}
    <Player player />
  {/each} -->
</div>