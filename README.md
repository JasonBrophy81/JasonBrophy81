import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";

export default function TipCalculator() {
  const [bill, setBill] = useState("");
  const [tip, setTip] = useState(15);
  const [total, setTotal] = useState(0);

  const calculateTotal = () => {
    const billAmount = parseFloat(bill);
    if (!isNaN(billAmount)) {
      const tipAmount = (billAmount * tip) / 100;
      setTotal(billAmount + tipAmount);
    }
  };

  return (
    <div className="flex items-center justify-center min-h-screen bg-gray-100">
      <Card className="p-6 w-96 shadow-lg bg-white rounded-2xl">
        <CardContent className="space-y-4">
          <h1 className="text-xl font-bold text-center">Tip Calculator</h1>
          <Input
            type="number"
            placeholder="Enter bill amount"
            value={bill}
            onChange={(e) => setBill(e.target.value)}
            className="w-full p-2 border rounded-md"
          />
          <div className="flex justify-between items-center">
            <label className="text-sm">Tip Percentage:</label>
            <select
              value={tip}
              onChange={(e) => setTip(parseInt(e.target.value))}
              className="p-2 border rounded-md"
            >
              {[5, 10, 15, 20, 25].map((percent) => (
                <option key={percent} value={percent}>{percent}%</option>
              ))}
            </select>
          </div>
          <Button className="w-full bg-blue-500 text-white p-2 rounded-md" onClick={calculateTotal}>
            Calculate
          </Button>
          {total > 0 && (
            <div className="text-center text-lg font-semibold">
              Total: ${total.toFixed(2)}
            </div>
          )}
        </CardContent>
      </Card>
    </div>
  );
}
