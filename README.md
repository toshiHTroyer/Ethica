# Ethica


# Data Model
`const EthicaSchema = new mongoose.Schema({
  // User Details
  users: [{
    username: {
      type: String,
      required: true,
      unique: true,
    },
    email: {
      type: String,
      required: true,
      unique: true,
    },
    slug: {
      type: String,
      required: true,
      unique: true,
    },
    profileImage: String,
    bio: String,
    socialLinks: {
      linkedin: String,
      instagram: String,
      personalWebsite: String,
    },
    savedExperiences: [{
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Experience'
    }],
    pastTrips: [{
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Trip'
    }],
    joinedAt: {
      type: Date,
      default: Date.now,
    }
  }],

  // Country and City Details
  countries: [{
    name: {
      type: String,
      required: true,
      unique: true,
    },
    slug: {
      type: String,
      required: true,
      unique: true,
    },
    blurb: {
      type: String,
      required: true,
    },
    cities: [{
      name: {
        type: String,
        required: true,
      },
      slug: {
        type: String,
        required: true,
        unique: true,
      },
      blurb: String,
      foodExperiences: [{
        type: mongoose.Schema.Types.ObjectId,
        ref: 'Experience'
      }],
      travelExperiences: [{
        type: mongoose.Schema.Types.ObjectId,
        ref: 'Experience'
      }],
      nightlife: [{
        type: mongoose.Schema.Types.ObjectId,
        ref: 'Experience'
      }],
      localHosts: [{
        type: mongoose.Schema.Types.ObjectId,
        ref: 'Experience'
      }],
    }]
  }],

  // Experience Details
  experiences: [{
    name: {
      type: String,
      required: true,
    },
    description: String,
    category: {
      type: String,
      enum: ['Food', 'Travel', 'Nightlife', 'Local Host', 'Activity'],
      required: true,
    },
    images: [String],
    location: {
      countrySlug: {
        type: String,
        required: true,
      },
      citySlug: {
        type: String,
        required: true,
      }
    },
    price: Number,
    ratings: [{
      user: {
        type: mongoose.Schema.Types.ObjectId,
        ref: 'User',
      },
      rating: {
        type: Number,
        min: 1,
        max: 5,
      },
      comment: String,
      date: {
        type: Date,
        default: Date.now,
      }
    }],
    ethicalIndicators: [String], // e.g., 'eco-friendly', 'women-owned', 'locally-run'
    createdAt: {
      type: Date,
      default: Date.now,
    }
  }],

  // Trip Details (Directly Linked to Users)
  trips: [{
    user: {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'User',
      required: true,
    },
    experiences: [{
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Experience'
    }],
    startDate: Date,
    endDate: Date,
    notes: String,
    createdAt: {
      type: Date,
      default: Date.now,
    }
  }]
});

module.exports = mongoose.model('Ethica', EthicaSchema);`
