# OIL-GAS-INDUSTRY-BEST-PRACTICES-ADVISOR
OIL &amp; GAS INDUSTRY BEST PRACTICES ADVISOR
import React, { useState, useEffect } from 'react';

interface Recommendation {
  id: number;
  title: string;
  description: string;
  pillar: string;
  priority: 'High' | 'Medium' | 'Low';
  status: 'Open' | 'In Progress' | 'Completed';
}

const initialRecommendations: Recommendation[] = [
  {
    id: 1,
    title: 'Reduce Methane Emissions',
    description: 'Implement leak detection and repair (LDAR) programs across all facilities to minimize methane emissions.',
    pillar: 'Sostenibilidad y Medio Ambiente',
    priority: 'High',
    status: 'Open',
  },
  {
    id: 2,
    title: 'Predictive Maintenance for Pumps',
    description: 'Use AI-powered predictive maintenance to identify potential pump failures and schedule maintenance proactively.',
    pillar: 'Eficiencia Operativa y Optimización',
    priority: 'Medium',
    status: 'In Progress',
  },
  {
    id: 3,
    title: 'Safety Training on H2S Handling',
    description: 'Conduct comprehensive safety training on the safe handling of hydrogen sulfide (H2S) for all personnel.',
    pillar: 'Seguridad Industrial y Protección del Personal',
    priority: 'High',
    status: 'Open',
  },
  {
    id: 4,
    title: 'Market Analysis for Crude Oil Futures',
    description: 'Analyze market trends and crude oil futures to optimize buying and selling strategies.',
    pillar: 'Gestión Financiera y Transparencia',
    priority: 'Medium',
    status: 'Completed',
  },
  {
    id: 5,
    title: 'AI for Reservoir Characterization',
    description: 'Apply AI and machine learning techniques for enhanced reservoir characterization and evaluation of reserves.',
    pillar: 'Innovación y Transformación Digital',
    priority: 'Medium',
    status: 'In Progress',
  },
  {
    id: 6,
    title: 'Community Engagement Program',
    description: 'Develop and implement a community engagement program to address local concerns and promote social responsibility.',
    pillar: 'Relación con Comunidades y Responsabilidad Social',
    priority: 'Low',
    status: 'Open',
  },
];

const OilAndGasAdvisor = () => {
  const [recommendations, setRecommendations] = useState<Recommendation[]>(initialRecommendations);
  const [selectedPillar, setSelectedPillar] = useState<string>('All');
  const [searchTerm, setSearchTerm] = useState<string>('');

  const handleStatusChange = (id: number, newStatus: Recommendation['status']) => {
    setRecommendations(
      recommendations.map((rec) =>
        rec.id === id ? { ...rec, status: newStatus } : rec
      )
    );
  };

  const handlePriorityChange = (id: number, newPriority: Recommendation['priority']) => {
    setRecommendations(
      recommendations.map((rec) =>
        rec.id === id ? { ...rec, priority: newPriority } : rec
      )
    );
  };


  const filteredRecommendations = recommendations.filter((rec) => {
    const pillarFilter = selectedPillar === 'All' || rec.pillar === selectedPillar;
    const searchFilter = rec.title.toLowerCase().includes(searchTerm.toLowerCase()) ||
      rec.description.toLowerCase().includes(searchTerm.toLowerCase());

    return pillarFilter && searchFilter;
  });


  const pillars = ['All', ...Array.from(new Set(recommendations.map((rec) => rec.pillar)))];

  return (
    <div className="bg-gray-100 min-h-screen p-8">
      <h1 className="text-3xl font-semibold text-gray-800 mb-6">
        Oil & Gas Industry Best Practices Advisor
      </h1>

      <div className="flex flex-col md:flex-row items-center justify-between mb-4">
        <div className="flex items-center mb-2 md:mb-0">
          <label htmlFor="pillarFilter" className="mr-2 text-gray-700">Filter by Pillar:</label>
          <select
            id="pillarFilter"
            className="p-2 border rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none"
            value={selectedPillar}
            onChange={(e) => setSelectedPillar(e.target.value)}
          >
            {pillars.map((pillar) => (
              <option key={pillar} value={pillar}>
                {pillar}
              </option>
            ))}
          </select>
        </div>

        <div className="flex items-center">
          <label htmlFor="searchInput" className="mr-2 text-gray-700">Search:</label>
          <input
            type="text"
            id="searchInput"
            placeholder="Search recommendations..."
            className="p-2 border rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none"
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
          />
        </div>
      </div>

      <div className="grid gap-4 grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
        {filteredRecommendations.map((recommendation) => (
          <div key={recommendation.id} className="bg-white rounded-lg shadow-md p-4">
            <h2 className="text-xl font-semibold text-gray-800 mb-2">
              {recommendation.title}
            </h2>
            <p className="text-gray-600 mb-4">{recommendation.description}</p>
            <div className="mb-2">
              <span className="font-semibold text-gray-700">Pillar:</span>{' '}
              {recommendation.pillar}
            </div>
            <div className="flex items-center justify-between mb-2">
              <div>
                <span className="font-semibold text-gray-700">Priority:</span>
                <select
                  value={recommendation.priority}
                  onChange={(e) =>
                    handlePriorityChange(recommendation.id, e.target.value as Recommendation['priority'])
                  }
                  className="ml-2 p-1 border rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none"
                >
                  <option value="High">High</option>
                  <option value="Medium">Medium</option>
                  <option value="Low">Low</option>
                </select>
              </div>
            </div>
            <div className="flex items-center justify-between">
              <div>
                <span className="font-semibold text-gray-700">Status:</span>
                <select
                  value={recommendation.status}
                  onChange={(e) =>
                    handleStatusChange(recommendation.id, e.target.value as Recommendation['status'])
                  }
                  className="ml-2 p-1 border rounded-md shadow-sm focus:ring focus:ring-indigo-200 focus:outline-none"
                >
                  <option value="Open">Open</option>
                  <option value="In Progress">In Progress</option>
                  <option value="Completed">Completed</option>
                </select>
              </div>
            </div>
          </div>
        ))}
      </div>
    </div>
  );
};

export default OilAndGasAdvisor;
