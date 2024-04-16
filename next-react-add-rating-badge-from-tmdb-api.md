### Add Rating Badge with Rating from TMDB

## Rating Badge Component
```jsx
import React from 'react';

function RatingBadge({ rating }: { rating: string }) {
  const colors = {
    G: "#016936",
    PG: "#F25A24",
    "PG-13": "#803D9A",
    R: "#D8131B",
    "NC-17": "#1B3E9C",
  };

  return (
    <div className="flex ml-2 scale-75">
      <div
        className="px-1 min-w-5 flex justify-center items-center bg-opacity-50 rounded-[2px] text-white"
        style={{
          backgroundColor: colors[rating.toUpperCase().trim()] ?? "black",
          opacity: 0.75,
        }}
      >
        <p className="text-[14px] font-bold">{rating}</p>
      </div>
    </div>
  );
}

export default RatingBadge;
```

The `RatingBadge` component takes a `rating` prop of type `string` and displays a movie rating badge with a specific color based on the rating value.

You can use the `RatingBadge` component in your movie details component with the provided implementation for grabbing the rating:

```jsx
import React from 'react';
import RatingBadge from './RatingBadge';

const MovieDetails = ({ movie }) => {
  const release_dates = movie.release_dates?.results;
  let rating = "NR";

  if (release_dates.length > 0) {
    let found = release_dates.find((date) => date.iso_3166_1 === "US");
    if (found) {
      // Find where certification is not empty or null
      let temp = found.release_dates.find((date) => date.certification !== "");
      rating = temp.certification ?? found.release_dates[0].certification;
    }
  }

  return (
    <div>
      <h2>{movie.title}</h2>
      <RatingBadge rating={rating} />
      {/* Other movie details */}
    </div>
  );
};

export default MovieDetails;
```

The rating is extracted from the movie's `release_dates` data using the provided implementation.

The code first checks if `release_dates` exists and has a length greater than 0. If so, it tries to find the release date information for the "US" country using the `find` method.

If the "US" release date information is found, it further searches for a release date with a non-empty certification value. If a non-empty certification is found, it assigns that value to the `rating` variable. If no non-empty certification is found, it falls back to the certification of the first release date entry.

Finally, the `rating` is passed as a prop to the `RatingBadge` component, which displays the rating badge with the corresponding color based on the rating value. If no valid rating is found, it defaults to "NR" (Not Rated).

Happy coding!