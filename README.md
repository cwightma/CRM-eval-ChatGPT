# CRM-eval-ChatGPT
import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Tabs, TabsList, TabsTrigger, TabsContent } from "@/components/ui/tabs";
import { BarChart, Bar, XAxis, YAxis, Tooltip, ResponsiveContainer } from "recharts";

const competitors = [
  {
    name: "Reunitus",
    product: "Lost to Found",
    strengths: ["50+ years expertise", "AirTag integration", "Compliance ready"],
    weaknesses: ["Higher complexity", "Enterprise-only focus"],
    rating: 4.9,
    globalReach: "High",
    aiLevel: "Moderate",
  },
  {
    name: "Boomerang",
    product: "Boomerang Network",
    strengths: ["AI-driven", "Celebrity investors", "Venue partnerships"],
    weaknesses: ["Startup risk", "US-only initially"],
    rating: 4.8,
    globalReach: "Medium",
    aiLevel: "High",
  },
  {
    name: "iLost",
    product: "iLost for Business",
    strengths: ["18 language support", "ISO certified", "High usability"],
    weaknesses: ["Small team", "Limited PR presence"],
    rating: 4.7,
    globalReach: "High",
    aiLevel: "Low",
  },
];

const sentimentData = competitors.map((c) => ({ name: c.name, rating: c.rating }));

export default function LostFoundCRMApp() {
  const [selected, setSelected] = useState("overview");

  return (
    <div className="p-6 space-y-6 max-w-6xl mx-auto">
      <h1 className="text-3xl font-bold text-center">Lost & Found CRM Market Explorer</h1>
      <Tabs value={selected} onValueChange={setSelected}>
        <TabsList className="flex justify-center flex-wrap gap-2">
          <TabsTrigger value="overview">Market Overview</TabsTrigger>
          <TabsTrigger value="compare">Compare Competitors</TabsTrigger>
          <TabsTrigger value="recommend">Strategic Recommendations</TabsTrigger>
        </TabsList>

        <TabsContent value="overview">
          <Card>
            <CardContent className="prose max-w-none p-4">
              <h2>Emerging Trends</h2>
              <ul>
                <li>AI-enhanced item matching</li>
                <li>IoT integrations like AirTags</li>
                <li>Customer experience via automation</li>
                <li>Global expansion with multilingual support</li>
                <li>Network-based lost item systems</li>
              </ul>
              <h2>Customer Sentiment</h2>
              <ResponsiveContainer width="100%" height={300}>
                <BarChart data={sentimentData}>
                  <XAxis dataKey="name" />
                  <YAxis domain={[4.5, 5]} />
                  <Tooltip />
                  <Bar dataKey="rating" fill="#4f46e5" />
                </BarChart>
              </ResponsiveContainer>
            </CardContent>
          </Card>
        </TabsContent>

        <TabsContent value="compare">
          <div className="grid md:grid-cols-3 gap-4">
            {competitors.map((c) => (
              <Card key={c.name}>
                <CardContent className="p-4">
                  <h3 className="text-xl font-semibold">{c.name}</h3>
                  <p className="text-sm text-muted-foreground">{c.product}</p>
                  <div className="mt-2">
                    <strong>Strengths:</strong>
                    <ul className="list-disc pl-5">
                      {c.strengths.map((s, i) => (
                        <li key={i}>{s}</li>
                      ))}
                    </ul>
                    <strong>Weaknesses:</strong>
                    <ul className="list-disc pl-5">
                      {c.weaknesses.map((w, i) => (
                        <li key={i}>{w}</li>
                      ))}
                    </ul>
                    <p className="mt-2"><strong>AI Level:</strong> {c.aiLevel}</p>
                    <p><strong>Global Reach:</strong> {c.globalReach}</p>
                  </div>
                </CardContent>
              </Card>
            ))}
          </div>
        </TabsContent>

        <TabsContent value="recommend">
          <Card>
            <CardContent className="prose max-w-none p-4">
              <h2>Top Recommendation</h2>
              <p><strong>Best Overall:</strong> <span className="text-indigo-600">Reunitus – Lost to Found</span></p>
              <p>
                Reunitus offers unmatched enterprise depth, regulatory features, and integration support (e.g., AirTag, compliance).
                Ideal for global businesses that require full lifecycle management.
              </p>
              <h2>When to Choose Others</h2>
              <ul>
                <li><strong>Boomerang:</strong> If AI-powered automation, fast rollout, and U.S. entertainment/hospitality focus is preferred.</li>
                <li><strong>iLost:</strong> If you prioritize multilingual support, ISO security, and ease of integration for global airports or rail.</li>
              </ul>
            </CardContent>
          </Card>
        </TabsContent>
      </Tabs>
    </div>
  );
}
