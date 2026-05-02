import React from "react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button"; import { Trophy, Wallet, BarChart3 } from "lucide-react";

const matches = [ { team1: "Arsenal", team2: "Chelsea", odds1: 2.1, odds2: 3.4 }, { team1: "Real Madrid", team2: "Barcelona", odds1: 1.9, odds2: 2.8 }, { team1: "Lakers", team2: "Warriors", odds1: 2.3, odds2: 2.0 }, ];

export default function SportsBettingSite() { return ( <div className="min-h-screen bg-gray-100 p-6"> <header className="flex items-center justify-between mb-8"> <h1 className="text-3xl font-bold">Sportbet</h1> <Button className="rounded-2xl px-6">Login</Button> </header>

<section className="grid md:grid-cols-3 gap-4 mb-8">
    <Card className="rounded-2xl shadow-md">
      <CardContent className="p-6 flex items-center gap-4">
        <Wallet className="w-8 h-8" />
        <div>
          <p className="text-sm text-gray-500">Balance</p>
          <h2 className="text-xl font-semibold">$1,250</h2>
        </div>
      </CardContent>
    </Card>

    <Card className="rounded-2xl shadow-md">
      <CardContent className="p-6 flex items-center gap-4">
        <Trophy className="w-8 h-8" />
        <div>
          <p className="text-sm text-gray-500">Wins</p>
          <h2 className="text-xl font-semibold">24 Bets</h2>
        </div>
      </CardContent>
    </Card>

    <Card className="rounded-2xl shadow-md">
      <CardContent className="p-6 flex items-center gap-4">
        <BarChart3 className="w-8 h-8" />
        <div>
          <p className="text-sm text-gray-500">Profit</p>
          <h2 className="text-xl font-semibold">+$420</h2>
        </div>
      </CardContent>
    </Card>
  </section>

  <section>
    <h2 className="text-2xl font-semibold mb-4">Live Matches</h2>
    <div className="grid gap-4">
      {matches.map((match, index) => (
        <Card key={index} className="rounded-2xl shadow-md">
          <CardContent className="p-6 flex flex-col md:flex-row md:items-center md:justify-between gap-4">
            <div>
              <h3 className="text-lg font-semibold">
                {match.team1} vs {match.team2}
              </h3>
              <p className="text-sm text-gray-500">Place your bet now</p>
            </div>

            <div className="flex gap-3">
              <Button className="rounded-xl px-5">
                {match.team1} ({match.odds1})
              </Button>
              <Button variant="outline" className="rounded-xl px-5">
                {match.team2} ({match.odds2})
              </Button>
            </div>
          </CardContent>
        </Card>
      ))}
    </div>
  </section>
</div>

); }
