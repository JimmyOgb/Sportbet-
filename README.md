import React from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Trophy, Wallet, Percent, Flame } from "lucide-react";
import { motion } from "framer-motion";

const matches = [
  { home: "Arsenal", away: "Chelsea", odds: ["2.10", "3.40", "3.00"] },
  { home: "Real Madrid", away: "Barcelona", odds: ["2.45", "3.20", "2.80"] },
  { home: "Man City", away: "Liverpool", odds: ["1.95", "3.60", "3.50"] },
  { home: "PSG", away: "Bayern", odds: ["2.30", "3.10", "2.95"] },
];

export default function Bet9jaInspiredHomepage() {
  return (
    <div className="min-h-screen bg-zinc-950 text-white">
      <header className="border-b border-zinc-800 bg-zinc-900 sticky top-0 z-50">
        <div className="max-w-7xl mx-auto px-6 py-4 flex items-center justify-between">
          <h1 className="text-2xl font-bold tracking-wide text-green-400">
            SportBet
          </h1>
          <div className="flex gap-3">
            <Button className="rounded-2xl">Login</Button>
            <Button variant="outline" className="rounded-2xl text-black bg-white">
              Register
            </Button>
          </div>
        </div>
      </header>

      <section className="max-w-7xl mx-auto px-6 py-10 grid md:grid-cols-3 gap-6">
        <motion.div
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          className="md:col-span-2"
        >
          <Card className="rounded-3xl bg-gradient-to-r from-green-500 to-emerald-700 border-0 shadow-xl">
            <CardContent className="p-8">
              <h2 className="text-4xl font-bold mb-3">Welcome to SportBet</h2>
              <p className="text-lg opacity-90 mb-6">
                Fast betting, live odds, instant withdrawals and exciting jackpots.
              </p>
              <Button className="rounded-2xl bg-white text-black hover:bg-zinc-200">
                Start Betting
              </Button>
            </CardContent>
          </Card>
        </motion.div>

        <div className="space-y-4">
          {[
            { icon: Wallet, title: "Fast Withdrawals" },
            { icon: Percent, title: "High Winning Odds" },
            { icon: Flame, title: "Daily Jackpots" },
          ].map((item, index) => (
            <Card key={index} className="rounded-2xl bg-zinc-900 border-zinc-800">
              <CardContent className="p-5 flex items-center gap-4">
                <item.icon className="w-6 h-6 text-green-400" />
                <p className="font-medium">{item.title}</p>
              </CardContent>
            </Card>
          ))}
        </div>
      </section>

      <section className="max-w-7xl mx-auto px-6 pb-12">
        <div className="flex items-center gap-2 mb-6">
          <Trophy className="text-green-400" />
          <h3 className="text-2xl font-semibold">Top Matches</h3>
        </div>

        <div className="grid gap-4">
          {matches.map((match, index) => (
            <Card key={index} className="rounded-2xl bg-zinc-900 border-zinc-800">
              <CardContent className="p-5 grid md:grid-cols-4 gap-4 items-center">
                <div className="md:col-span-2">
                  <p className="font-semibold text-lg">
                    {match.home} vs {match.away}
                  </p>
                  <p className="text-sm text-zinc-400">Live Betting Available</p>
                </div>

                <div className="flex gap-2">
                  {match.odds.map((odd, i) => (
                    <Button
                      key={i}
                      variant="outline"
                      className="rounded-xl border-zinc-700 w-full"
                    >
                      {odd}
                    </Button>
                  ))}
                </div>

                <Button className="rounded-2xl bg-green-500 hover:bg-green-600">
                  Add to Betslip
                </Button>
              </CardContent>
            </Card>
          ))}
        </div>
      </section>
    </div>
  );
}
